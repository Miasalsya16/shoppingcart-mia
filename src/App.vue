<template>
  <div id="app" style="background-color: #F5F5F5;">
    <HeaderComponent />
    <div class="main" style="background-color: #F5F5F5;">
      <div class="container-fluid" style="background-color: #F5F5F5;">
        <div class="row">
          <div class="col-12 col-lg-8"><ShopComponent /></div>
        <!-- </div>
        <div class="row pb-4 justify-content-lg-center"> -->
          <div class="col-12 col-lg-4 "><CartComponent /></div>
        </div> 
      </div>
    </div>
 </div>
</template>

<script>
import ShopComponent from "./components/ShopComponent.vue";
import CartComponent from "./components/CartComponent.vue";
import HeaderComponent from "./components/HeaderComponent.vue";

export default {
  name: "App",
  components: {
    ShopComponent,
    CartComponent,
    HeaderComponent
},
};
</script>

<style>
#app {
  text-align: center;
}
</style>
