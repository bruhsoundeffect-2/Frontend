<template>
  <div>
    <button class="btn btn-primary navbar-btn" data-toggle="modal" data-target="#shoppingCart">
      <i class="fa fa-shopping-cart" aria-hidden="true"></i>
      ({{ numInCart }})
    </button>
    <div class="modal fade" id="shoppingCart" tabindex="-1" role="dialog" aria-labelledby="shoppingCartLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="shoppingCartLabel">Current order</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <table class="table">
              <tbody>
              <tr v-for="(item,idx) in inCart" :key="idx">
                <td>{{ item.title }}</td>
                <td>${{ item.price }}</td>
                <td>
                  <button class="btn btn-sm btn-danger" @click="removeFromCart(item)">&times;</button>
                </td>
              </tr>
              <tr>
                <th></th>
                <th>${{ total }}</th>
                <th></th>
              </tr>
              </tbody>
            </table>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Back to shop</button>
            <button type="button" class="btn btn-primary">Order</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>

export default {
  name: 'ShoppingCart',
  computed: {
    inCart() {
      return this.$store.getters.inCart;
    },
    numInCart() {
      return this.inCart.length;
    },
    total() {
      return this.inCart.reduce((acc, cur) => acc + cur.price, 0);
    },
    isAuthenticated() {
      return this.$store.state.user.isAuthenticated;
    },
  },
  methods: {
    removeFromCart(item) {
      this.$store.commit('removeFromCart', item);
    },
    checkout() {
      if (this.isAuthenticated) {
        if (this.numInCart === 0) {
          alert('Your cart is empty!');
          return
        }
      } else {
        alert('Please login to checkout');
        return
      }
    },
  }
};
</script>