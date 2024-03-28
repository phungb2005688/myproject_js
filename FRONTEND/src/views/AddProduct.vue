
<script>
import toastjs from "../assets/js/toasts";
import toastsVue from "../components/toasts.vue";
import ProductService from "../services/Product.service";
import Productform from "../components/Productform.vue";
export default {
  data() {
    return {
      toasts: {
        title: "Success",
        msg: "Thêm sản phẩm thành công",
        type: "success",
        duration: 2000
      },
    }
  },
  components: {
    Productform,
    toastsVue
  },
  methods: {
    toastjs,
    async addproduct(data) {
      try {
        await ProductService.create(data);
        this.toastjs();
        setTimeout(() => {
          location.reload();
        }, 2000);
      } catch (error) {
        console.log(error);
        this.toasts.title = "Warning",
          this.toasts.msg = "Tài khoản không phải ADMIN",
          this.toasts.type = "warn",
          this.toasts.duration = 2000
        this.toastjs();
      }
    },
  },
};
</script>
<template>
  <div style="padding-bottom: 0px;">
    <div class="container-fluid" style="background-color: #E4F1FF;">
      <div style="height: 59px;">
        <nav class="navbar navbar-expand-lg navbar-dark">

          <a class="navbar-brand" href="">
            <router-link to="/admin" class="text text-decoration-none"> TRANG CHỦ</router-link>
          </a>
          <a class="navbar-brand" href="">
            <router-link to="/ListKH" class="text">QUẢN LÝ NGƯỜI DÙNG</router-link>
          </a>
          <a class="navbar-brand" href="">
            <router-link to="/ListSP" class="text">QUẢN LÝ SẢN PHẨM</router-link>
          </a>
          <router-link to="/">
            <img src="../assets/img/LGA.png" style=" margin-left: 420px; width: 150px; height: 50px; margin-top: -6px;"
              alt="">
          </router-link>

        </nav>
      </div>

    </div>
  </div>

  <div class="page">
    <div style="background-color: #fafafa;">
      <div style="padding-top: 10px;">
        <div style="margin-left: 500px;">
          <h4 class="titleh4">THÊM SẢN PHẨM</h4>
        </div>
      </div>

      <Productform :product="{ img: [] }" @submit:product="addproduct" :resetAfterSubmit="false" />
    </div>
  </div>
  <toastsVue></toastsVue>
</template>
<style>
.titleh4 {
  text-align: center;
  color: #fff;
  margin-top: 10px;
  border: 1px solid #2e1c11;
  background-color: #2e1c11;
  width: 330px;
  padding: 5px;
  border-radius: 10px;
}

.text {
  height: 150px;
  color: #2e1c11;
  margin-left: 10px;
  font-weight: 700;
  padding: 17px;
  font-size: 17px;
}

.text:hover {
  color: #2e1c11;
  margin-left: 10px;
  background-color: #fff;
  padding: 17px;
  font-size: 17px;
}
</style>
