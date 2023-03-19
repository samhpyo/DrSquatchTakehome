<template>
  <div class="App">
    <div class="Header">
      <CheckboxSearch @updateScents="filterScents" :scents="scents" />
      <!-- <template v-for="(scent, index) in scents" :key="index">
        <input type="checkbox" v-model="selectedScents" :value="scent" class="CheckBox" />
        <span class="FilterName">{{ scent.charAt(0).toUpperCase() + scent.slice(1) }}</span>
      </template> -->
    </div>
    <div class="Bundles" v-if="device === `Desktop`">
      <div v-for="bundle in filteredScent" :key="bundle.handle">
        <BundleCard :bundle="bundle" :device="device" />
      </div>
    </div>
    <div class="BundlesMobile" v-else>
      <div v-for="bundle in filteredScent" :key="bundle.handle">
        <BundleCard :bundle="bundle" :device="device" />
      </div>
    </div>
  </div>
</template>

<script>
import BundleCard from '@/components/Card.vue'
import CheckboxSearch from '@/components/Search.vue'
export default {
  name: 'App',
  components: {
    BundleCard,
    CheckboxSearch
  },
  data() {
    return {
      bundles: [],
      modifiedBundles: [],
      scents: [],
      prices: [],
      bundleName: '',
      selectedScents: [],
      device: 'Desktop'
    }
  },
  computed: {
    filteredScent() {
      if (!this.selectedScents.length) return this.bundles
      return this.bundles.filter((bundle) =>
        bundle.scent.some((scent) => this.selectedScents.includes(scent))
      )
    }
  },
  methods: {
    filterScents(array) {
      // console.log('array', array)
      this.selectedScents = array
    },
    screenResize() {
      let size = window.innerWidth
      if (size < 481) {
        this.device = 'Phone'
      }
      if (size > 480 && size < 1025) {
        this.device = 'Tablet'
      }
      if (size > 1024) {
        this.device = 'Desktop'
      }
    },
    async fetchData() {
      const response = await fetch(`https://ae3t7l1i79.execute-api.us-east-1.amazonaws.com/bundles`)
      const data = await response.json()
      return data
    },
    async fetchProductData(product) {
      const response = await fetch(
        `https://ae3t7l1i79.execute-api.us-east-1.amazonaws.com/product/${product}`
      )
      const data = await response.json()
      return data
    },
    async bundleList() {
      const data = await this.fetchData()
      this.bundles = data
    },
    async productList(product) {
      const data = await this.fetchProductData(product)
      const dataObj = {
        title: data.title,
        price: data.price,
        scent: data.scent_profile
      }
      return dataObj
    },
    addIncludedItemText(bundle) {
      if (!bundle) return
      const obj = {}
      let string = ''
      bundle.titles.forEach((title) => {
        if (!obj[title]) {
          obj[title] = 1
        } else obj[title] += 1
      })
      let array = Object.entries(obj)
      Object.entries(obj).forEach((entry, index) => {
        const [key, value] = entry
        if (value === 1) {
          if (index === 0) string = `${key}`
          else if (index === array.length - 1) string += `, and ${key}`
          else string += `, ${key}`
        } else {
          if (index === 0) string = `${key} x ${value}`
          else if (index === array.length - 1) string += `, and ${key} x ${value}`
          else string += `, ${key} x ${value}`
        }
      })
      return string
    }
  },
  async created() {
    this.screenResize()
    await this.bundleList()
    this.bundles.forEach((bundle) => {
      bundle.products_included.forEach(async (product) => {
        const result = await this.productList(product)
        if (!bundle.originalPrice) bundle.originalPrice = result.price
        else bundle.originalPrice += result.price
        if (bundle.scent) {
          result.scent.forEach((scent) => {
            if (!this.scents.includes(scent)) this.scents.push(scent)
            if (!bundle.scent.includes(scent)) {
              bundle.scent.push(scent)
            }
          })
        } else bundle.scent = result.scent
        if (!bundle.titles) bundle.titles = [result.title]
        else bundle.titles.push(result.title)
        const extras = this.addIncludedItemText(bundle)
        bundle.includedItems = extras
      })
    })
  },
  mounted() {
    window.addEventListener('resize', this.screenResize)
  },
  unmounted() {
    window.removeEventListener('resize', this.screenResize)
  }
}
</script>
<style>
.Header {
  position: flex;
  top: 0px;
  margin-top: 20px;
  margin-left: 20px;
}
.Bundles {
  box-sizing: border-box;
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.BundlesMobile {
  box-sizing: border-box;
  display: grid;
  grid-template-columns: 1fr;
}
</style>
