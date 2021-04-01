<template>
  <nav class="navbar navbar-expand-lg navbar-light fixed-top" role="navigation" id="mainNav">
    <div class="container">
      <router-link to="/" class="navbar-brand js-scroll-trigger">Password Serial Bus</router-link>
      <ul class="navbar-nav mr-auto">
      </ul>
      <ul class="nav navbar-nav">
        <button class="navbar-toggler navbar-toggler-right" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
          Menu
          <i class="fas fa-bars"></i>
        </button>
        <div class="collapse navbar-collapse" id="navbarResponsive">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item"><a class="nav-link js-scroll-trigger" href="http://landing-page-ucllteam11.ocp-ucll-40cb0df2b03969eabb3fac6e80373775-0000.eu-de.containers.appdomain.cloud">Landing page</a></li>
            <li class="nav-item"><router-link to="/" tag="li" v-if="!isAuthenticated" active-class="active"><a @click="onLoginClicked" class="nav-link">Login</a>
            </router-link></li>
            <li class="nav-item mt-4"><ShoppingCart/></li>
            <li v-if="isAuthenticated" class="li-pointer nav-item mt-4">
              <div class="dropdown">
                <button class="btn btn-secondary dropdown-toggle ml-1" type="button" id="dropdownMenuButton" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                  {{ getUserName() }}
                </button>
                <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                  <a v-if="isPartner" @click="onRegisterClicked" class="dropdown-item" href="#">Register Product</a>
                  <a @click="onLogoutClicked" class="dropdown-item" style="color: black;">Logout {{ userEmail }}</a>
                </div>
              </div>
            </li>
          </ul>
        </div>
      </ul>
    </div>
  </nav>
</template>

<script>
import ShoppingCart from '@/ShoppingCart.vue';
export default {
  components: { ShoppingCart },
  name: 'NavHeader',
  computed: {
    userEmail() {
      return this.isLoggedIn ? this.currentUser.email : ''
    },
    isAuthenticated() {
      return this.$store.state.user.isAuthenticated;
    },
    isPartner() {
      return this.$store.state.user.partner;
    },
  },
  methods: {
    onLoginClicked() {
      window.location = this.$store.state.endpoints.login;
    },
    onLogoutClicked() {
      this.$store.commit("logout");
    },
    onRegisterClicked() {
      let obj = { 'description': 'description', 'id': parseInt("1"), 'price': parseInt("1000"), 'quantity': parseInt("10"), 'thumbnail_url': "thumbnail_url", 'title': "title" }
      this.$store.dispatch("registerProduct", obj);
    },
    getUserName() {
      return this.$store.state.user.name;
    }
  }
}
</script>