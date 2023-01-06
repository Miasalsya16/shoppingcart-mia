<template>
  <div class="cart nota mt-3">
    <div v-if="!cart.length" class="alert alert-secondary " role="alert">No Product in cart!</div>
    <div v-if="orderPlaced" @click="() => this.orderPlaced=false" class="alert alert-success alert-dismissible fade show" role="alert">
      Order successfully !
      <button type="button" class="close" data-dismiss="alert" aria-label="Close">
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Name</th>
          <th>QTY</th>
          <th>Price</th>
          <th>Sub Total</th>
          <th></th>
        </tr>
      </thead>
      <tbody class="align-middle">
        <tr v-for="item in cart" :key="item.id">
          <td>{{ item.title }}</td>
          <td>{{ item.qty }}</td>
          <td>$ {{ item.price }}</td>
          <td>$ {{ item.qty * item.price }}</td>
          <td>
            <ul class="list-group">
              <li class="list-group-item">
                <button @click="removeItemFromCart(item.id)" type="button" class="close" data-dismiss="modal" aria-label="Close">
                  <span aria-hidden="true">&times;</span>
                </button>
                <div class="media">
                  <div class="media-body">
                    <button class="qty-button btn btn-xs btn-outline-success" @click="reduceQty(item.id)">
                      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-dash-circle" viewBox="0 0 16 16">
                        <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
                          <path d="M4 8a.5.5 0 0 1 .5-.5h7a.5.5 0 0 1 0 1h-7A.5.5 0 0 1 4 8z"/>
                      </svg>
                    </button> {{ item.qty }}
                    <button class="qty-button btn btn-xs btn-outline-success" @click="addQty(item.id)">
                      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-plus-circle" viewBox="0 0 16 16">
                        <path d="M8 15A7 7 0 1 1 8 1a7 7 0 0 1 0 14zm0 1A8 8 0 1 0 8 0a8 8 0 0 0 0 16z"/>
                        <path d="M8 4a.5.5 0 0 1 .5.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3A.5.5 0 0 1 8 4z"/>
                      </svg>
                    </button>
                  </div>
                </div>
              </li>
             </ul>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="row justify-content-between" style="font-family: 'Roboto';">
      <div class="col-6 ">
        <h6 style="color:  #B6B6B6;">Total</h6>
      </div>
      <div class="col-6">
        <h6>$ {{ totalPrice.toLocaleString() }}</h6>
      </div>
    </div>
    <div class="mx-3 d-grid gap-2 pb-5">
      <button v-if="cart.length"  @click="placeOrder" class="checkout-button btn btn-lg btn-block add-cart" :disabled="isProcessing">
        <div v-if="isProcessing" class="spinner-border" role="status">
          <span class="sr-only">Loading...</span>
        </div>
        <span v-else>
          <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-cart" viewBox="0 0 16 16">
            <path d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM3.102 4l1.313 7h8.17l1.313-7H3.102zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
          </svg>  Checkout </span>
      </button>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "CartComponent",
  data() {
    return {
      isProcessing: false,
      orderPlaced: false
    };
  },
  computed: {
    ...mapGetters(["cart"]),
    totalPrice() {
      return this.cart.reduce((a, b) => a + b.qty * b.price, 0);
    },
    subtotalPrice() {
      let subtotal = 0;
      this.cart.ForEach((a,b) =>  { subtotal += a.qty * b.price; });
      return subtotal;
    }
  },
  methods: {
    ...mapActions(["removeItemFromCart", "addQty", "reduceQty", "emptyCart"]),
    placeOrder() {
      this.isProcessing = true;
      setTimeout(() => {
        this.isProcessing = false;
        this.orderPlaced = true;
        this.emptyCart();
      }, 1000);
    },
    
  }
};
</script>

<style scoped>
.media {
  width: 60%;
  text-align: left;
}

th{
  font-family: 'Roboto';
  font-style: normal;
  color: #7A7D85;

}
td{
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 16px;
  color: #B6B6B6;
}
.qty-button {
 width: 30px;
 height: 30px;
}

.checkout-button {
  margin-top: 20px;
}
.add-cart{
  background-color : #31C7CE;
  color: #FFFFFF;
}
.nota{
  background: #FFFFFF;
  box-shadow: 0px 15px 50px rgba(108, 146, 181, 0.1);
  border-radius: 25px;
}
</style>