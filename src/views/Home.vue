<template>
  <div class="container">
    <div class="container">
      <div class="row">
        <Item v-for="product in products"
        :key="product.id"
        :item="product"/>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  computed: {
    products() {
      return this.$store.state.products;
    }
  },
  components: {

  }
}
</script>
