<template>
        <div class="row">
        <div class="col-12 col-sm-6 col-md-3 col-lg-4 py-3 py-md-3 my-lg-0 py-3 py-md-3 my-lg-0" v-for="item in products" :key="item.id">
          <div class="card h-100" style="background-color: #FFFFFF" >
            <img :src="item.thumbnail" height="250" :alt="item.title" style="border-radius: 25px 25px 0px 0px;">
            <div class="text-start p-2 ps-3" style="background-color : #31C7CE; border-radius: 0px 0px 45px 0px;">
              <h4 class="smart " >{{ item.category }}</h4> 
            </div>
            <div class="d-flex flex-column card-body text-start">
              <h5 class="" style="font-family: 'Poppins'; color: #B6B6B6;"> {{ item.title }}</h5>
              <p class="card-title flex-grow-1" style="color: #404145;">{{ item.description }}</p>
              <!-- harga setelah diskon -->
              <div class="">
                <h4 class="pt-2 card-text" style="font-family: 'Poppins'; color: #404145;">$ {{ item.price }}</h4>               
                <button class="btn btn-dis btn-sm">{{ item.discountPercentage }}%</button> 
                <!-- harga sebelum diskon -->
                <s class="font-weight-light" style="color: #B6B6B6;">$ {{ priceBeforeDiscount(item) }}</s>
                <p class="py-2" style="color: #FFC226; font-family: 'Roboto';">
                  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" style="color: #FFC226;" class="bi bi-star-fill" viewBox="0 0 16 16">
                    <path d="M3.612 15.443c-.386.198-.824-.149-.746-.592l.83-4.73L.173 6.765c-.329-.314-.158-.888.283-.95l4.898-.696L7.538.792c.197-.39.73-.39.927 0l2.184 4.327 4.898.696c.441.062.612.636.282.95l-3.522 3.356.83 4.73c.078.443-.36.79-.746.592L8 13.187l-4.389 2.256z"/>
                  </svg>
                  {{ item.rating }}
                </p>
                <div class="d-grid gap-2 ">
                  <button class="btn add-cart btn-lg btn-100 font-weight-bold" style="font-family: 'Mulish';"  @click="addItemToCart(item)">
                    <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class="bi bi-cart" viewBox="0 0 16 16">
                      <path d="M0 1.5A.5.5 0 0 1 .5 1H2a.5.5 0 0 1 .485.379L2.89 3H14.5a.5.5 0 0 1 .491.592l-1.5 8A.5.5 0 0 1 13 12H4a.5.5 0 0 1-.491-.408L2.01 3.607 1.61 2H.5a.5.5 0 0 1-.5-.5zM3.102 4l1.313 7h8.17l1.313-7H3.102zM5 12a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm7 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4zm-7 1a1 1 0 1 1 0 2 1 1 0 0 1 0-2zm7 0a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"/>
                    </svg>  Add to cart
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  name: "ShopComponent",
  mounted() {
    this.getProducts();
  },
  computed: {
    ...mapGetters(["products"]),
    //   discountedPrice(item) {
  //   return  (item.price *(item.discountPercentage)/100)
  // }
  },
  methods: {
    ...mapActions(["addItemToCart", "getProducts"]),
    priceBeforeDiscount(item){
      let price = 100 / (100 - item.discountPercentage) * item.price;
      return price.toFixed(2);
    },
    
  },
  data(){
            return{
                produk:[],
                  
            }
        },
  created(){
      // this.$axios.get('https://dummyjson.com/products')
      // .then((response) => {
      //     this.produk = response.data.data
      // })
  },
};
</script>

<style scoped>
.card {
  border: none;
}
.smart{
  font-family: 'Poppins';
  font-style: normal;
  line-height: 24px;
  color: #FFFFFF;
}
.add-cart{
  background-color : #31C7CE;
  color: #FFFFFF;
}
.btn-dis{
  background-color : #FFDBE2;
  color: #ED3C47;
}

</style>
