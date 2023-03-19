<template>
  <div v-for="(scent, index) in this.scents" :key="index" class="Search">
    <div>
      <input
        type="checkbox"
        :value="scent"
        class="CheckBox"
        @change="this.$emit('updateScents', this.selectedScents)"
        v-model="selectedScents"
      />
      <span class="FilterName">{{ scent.charAt(0).toUpperCase() + scent.slice(1) }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CheckboxSearch',
  props: {
    scents: Array
  },
  data() {
    return {
      selectedScents: []
    }
  }
}
</script>
<style>
.Search{
  display: inline-block;
}
.FilterName {
  font-size: 25px;
  font-weight: 500;
  padding-right: 20px;
  padding-left: 5px;
}
</style>
