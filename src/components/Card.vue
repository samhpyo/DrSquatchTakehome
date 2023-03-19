<template>
  <div class="Card" v-if="device === `Desktop`">
    <img class="Image" :src="this.bundle.imageSrc" />
    <p class="Name">{{ this.bundle.title }}</p>
    <div class="Prices" v-if="this.bundle.originalPrice == this.bundle.price">
      <span class="PriceOnly">${{ this.bundle.price / 100 }}</span>
    </div>
    <div class="Prices" v-else>
      <span class="OriginalPrice">${{ this.bundle.originalPrice / 100 }}</span
      ><span class="Price">${{ this.bundle.price / 100 }}</span>
    </div>
    <span class="Scents">
      <span v-for="(scent, index) in this.bundle.scent" :key="index" :class="scent">
        {{ scent.toUpperCase() }}
      </span>
    </span>
    <span class="Included">Included</span>
    <p class="Products">{{ this.bundle.includedItems }}</p>
  </div>
  <div class="CardMobile" v-else>
    <img class="ImageMobile" :src="this.bundle.imageSrc" />
    <p class="Name">{{ this.bundle.title }}</p>
    <div class="Prices" v-if="this.bundle.originalPrice == this.bundle.price">
      <span class="PriceOnly">${{ this.bundle.price / 100 }}</span>
    </div>
    <div class="Prices" v-else>
      <span class="OriginalPrice">${{ this.bundle.originalPrice / 100 }}</span
      ><span class="Price">${{ this.bundle.price / 100 }}</span>
    </div>
    <a class="Scents">
      <ul v-for="(scent, index) in this.bundle.scent" :key="index" :class="`${scent}Mobile`">
        {{
          scent.toUpperCase()
        }}
      </ul>
    </a>
    <span class="Included">Included</span>
    <p class="Products">{{ this.bundle.includedItems }}</p>
  </div>
</template>
<script>
export default {
  name: 'BundleCard',
  props: {
    bundle: Object,
    device: String
  }
}
</script>
<style>
.Card {
  margin: 15px;
  width: 460px;
  height: 650px;
  padding: 20px;
  box-sizing: border-box;
  border: 1px solid gray;
  border-radius: 10px;
  display: grid;
  grid-template-rows: 1fr;
  grid-template-areas:
    'Image'
    'Name'
    'Prices'
    'Scents'
    'Products';
}
.CardMobile {
  margin: 15px;
  width: 410px;
  height: 500px;
  padding: 20px;
  box-sizing: border-box;
  border: 1px solid gray;
  border-radius: 10px;
  display: grid;
  grid-template-areas:
    'ImageMobile'
    'Name'
    'Prices'
    'Scents'
    'Products';
}
.ImageMobile {
  margin-left: 50px;
  height: 250px;
}
.Image {
  height: 400px;
  margin-left: -5px;
}
.Name {
  font-size: 30px;
  font-weight: 600;
}
.OriginalPrice {
  font-size: 20px;
  font-weight: 600;
  color: grey;
  text-decoration: line-through;
}
.Price {
  margin-left: -40px;
  font-size: 20px;
  font-weight: 600;
  color: green;
}
.PriceOnly{
  font-size: 20px;
  font-weight: 600;
  color: green;
}
.Prices {
  display: grid;
  grid-template-columns: 0.3fr 1fr;
  grid-template-areas: 'OriginalPrice' 'Price';
}
.Included {
  font-size: 20px;
  font-weight: 700;
}
.Products {
  font-size: 20px;
  font-weight: 500;
}
.Scents {
  color: white;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
}
.woodsy {
  background-color: #165834;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.fresh {
  background-color: 006fd6;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.citrus {
  background-color: #de7c00;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.herbal {
  background-color: #5a3714;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.spiced {
  background-color: #c10000;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.rich {
  background-color: #e0a17e;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
}
.woodsyMobile {
  background-color: #165834;
  border-radius: 15px;
  margin-right: 10px;
  padding-left: 10px;
  padding-right: 10px;
  font-size: 12px;
  padding-top: 2px;
}
.freshMobile {
  background-color: #006fd6;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
  padding-left: 10px;
  padding-right: 10px;
}
.citrusMobile {
  background-color: #de7c00;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
  padding-left: 10px;
  padding-right: 10px;
}
.herbalMobile {
  background-color: #5a3714;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
  padding-left: 10px;
  padding-right: 10px;
}
.spicedMobile {
  background-color: #c10000;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
  padding-left: 10px;
  padding-right: 10px;
}
.richMobile {
  background-color: #e0a17e;
  border-radius: 15px;
  margin-right: 10px;
  display: block;
  text-align: center;
  font-size: 12px;
  padding-top: 2px;
  padding-left: 10px;
  padding-right: 10px;
}
</style>
