<template>
  <Products :products="products" :error="error" />
</template>

<script>
import Products from "~/components/Products.vue"

export default {
  data() {
    return {
      products: [],
      error: null
    }
  },
  async mounted() {
    try {
      this.products = (await this.$strapi.$products.find({ 'filters[categories][id][$eq]' : this.$route.params.id, populate: '*'})).data
    } catch (error) {
      this.error = error
    }
  },
  components: {
    Products
  }
}
</script>
