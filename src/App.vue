<template>
  <div id="app">
    <NavHeader />
    <router-view style="margin-top: 6rem !important"/>
    <Footer />
  </div>
</template>

<script>
import NavHeader from "@/NavHeader.vue"
import Footer from "@/Footer.vue"
export default {
  components: {
    NavHeader,
    Footer
  },
  mounted(){
    this.$store.commit("setUrls");
    this.$store.dispatch("getProducts");
  }
}
</script>

<style>
#app {
  font-family: "Nunito", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
