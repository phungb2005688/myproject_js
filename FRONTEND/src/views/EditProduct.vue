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

          <img src="../assets/img/LGA.png" style=" margin-left: 420px; width: 150px; height: 50px; margin-top: -6px;"
            alt="">
        </nav>
      </div>

    </div>
  </div>
  <div v-if="product" class="page">
    <div style="padding-top: 10px;">
      <div style="margin-left: 500px;">
        <h4 class="titleh4">CHỈNH SỬA SẢN PHẨM</h4>
      </div>
    </div>
    <Productform :product="product" @submit:product="updateProduct" />
  </div>  
  <toastsVue></toastsVue>

</template>

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
        msg: "Sửa sản phẩm thành công",
        type: "success",
        duration: 2000
      },
      product: null,
    }
  },
  components: {
    Productform,
    toastsVue
  },
  methods: {
    toastjs,
    async getproduct(id) {
      try {
        this.product = await ProductService.get(id);
      } catch (error) {
        console.log(error);
        this.$router.push({
          name: "notfound",
          params: { pathMatch: this.$route.path.split("/").slice(1) },
          query: this.$route.query,
          hash: this.$route.hash,
        });
      }
    },
    async updateProduct(data) {
      try {
        await ProductService.update(this.product._id, data);
        this.toastjs();
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
  created() {
    this.getproduct(this.$route.params.id);
  }
};
</script>
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
</style>