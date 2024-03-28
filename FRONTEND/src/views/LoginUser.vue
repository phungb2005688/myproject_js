<script>
import FormloginVue from "../components/Formlogin.vue";
import toastsVue from "../components/toasts.vue";
import HeaderShop from '@/components/HeaderShop.vue'

export default {
  components: {
    FormloginVue,
    toastsVue,
    HeaderShop
  },
};
</script>
<template>
  <HeaderShop></HeaderShop>
  <toastsVue></toastsVue>
  <h2 class="loginn">ĐĂNG NHẬP </h2>
  <div class="h-100 mb-5">
    <div class="container">
      <div class="row d-flex justify-content-center align-items-center h-100">

        <!-- <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1"> -->
        <FormloginVue></FormloginVue>
        <!-- </div> -->
      </div>
    </div>
  </div>
</template>
<style>
.container {
  background-image: url(https://cdn.shopify.com/s/files/1/2364/6785/files/29_2f9c17c9-eea8-4c70-9c50-d1543ccf54f6.png?v=1571878313);
  height: 400px;
  width: 1000px;
}

.loginn {
  margin-top: 30px;
  text-align: center;
  color: #2E1C11;
}
</style>