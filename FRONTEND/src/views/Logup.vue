<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import AuthService from "../services/Auth.service";
import toast from "../assets/js/toasts";
import toastsVue from "../components/toasts.vue";
import HeaderShop from '@/components/HeaderShop.vue'

export default {
  components: {
    Form,
    Field,
    ErrorMessage,
    toastsVue, 
    HeaderShop
  },
  data() {
    const Logupform = yup.object().shape({
      name: yup
        .string()
        .required("Bạn chưa nhập Tên người dùng.")
        .min(4, "Tên phải ít nhất 4 ký tự."),
      email: yup
        .string()
        .required("Bạn chưa nhập Email.")
        .email("Email không hợp lệ.")
        .max(50, "Email có tối đa 50 ký tự."),
      pwd: yup
        .string()
        .required("Bạn chưa nhập Mật khẩu.")
    });
    return {
      Logupform,
      message: "Đăng ký thành công",
      usernew: {
        username: "",
        email: "",
        password: "",
      },
      toasts: {
        title: "",
        msg: "",
        type: "",
        duration: 0
      },
    };
  },
  methods: {
    toast,
    async postuser() {
      try {
        await AuthService.createsignup(this.usernew);
        this.toasts.title = "Success",
          this.toasts.msg = "Đăng ký thành công",
          this.toasts.type = "success",
          this.toasts.duration = 2000
        this.toast();
        setTimeout(() => {
          this.$router.push({ name: "login" });
        }, 2000);
      } catch (erorr) {
        console.log(erorr);
        this.toasts.title = "Faild",
          this.toasts.msg = "Thông tin bạn nhập đã được dùng",
          this.toasts.type = "error",
          this.toasts.duration = 2000
        this.toast();
      }
    }
  }
};
</script>

<template>
  <HeaderShop></HeaderShop>
  <toastsVue></toastsVue>
  <section class="text-center text-lg-start">
    <div class="container mb-5">
      <div class="align-items-center pt-4">
        <div class="">
          <div class="card cascading-right" style="
            background: hsla(0, 0%, 100%, 0.55); width: 710px; margin-left: 90px;
            /* backdrop-filter: blur(30px); */
            ">
            <div class="card-body shadow-5">
              <h2 class="loginn text-center mb-4">ĐĂNG KÝ </h2>

              <Form :validation-schema="Logupform">
                <div class="tentaikhoan form-outline mb-4">
                  <!-- <label class="form-label" for="name">Tên tài khoản</label> -->
                  <Field id="name" name="name" type="text" class="form-control" placeholder="Tên tài khoản"
                    v-model="usernew.username" />
                  <ErrorMessage name="name" class="text-danger" />
                </div>
                <div class="nhapemail mb-4">
                  <!-- <label class="form-label" for="email">Email</label> -->
                  <div class="form-outline">
                    <Field id="email" name="email" type="email" placeholder="Email" class="form-control"
                      v-model="usernew.email" />
                    <ErrorMessage name="email" class="text-danger" />
                  </div>
                </div>
                <div class="nhapmk form-outline">
                  <!-- <label class="form-label" for="pwd">Mật khẩu</label> -->
                  <Field id="pwd" name="pwd" type="password" class="form-control" placeholder="Mật khẩu"
                    v-model="usernew.password" />
                  <ErrorMessage name="pwd" class="text-danger" />
                </div>
                <div class="form-check d-flex justify-content-center mb-2">
                </div>
                <!-- Submit button -->
                <button type="button" class="btn btn-block mb-4 btn-sign" @click="postuser()">
                  Đăng Ký
                </button>
                <p class="small fw-bold mt-2 pt-1 mb-0" style="color: #2E1C11; margin-left: 200px;">Nếu bạn đã có tài khoản? 
                  <router-link class="dangnhap" to="/login"> Đăng nhập</router-link>
                </p>
              </Form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<style scoped  >
.container {
  background-image: url(https://cdn.shopify.com/s/files/1/2364/6785/files/29_2f9c17c9-eea8-4c70-9c50-d1543ccf54f6.png?v=1571878313);
  height: 450px;
  width: 900px;
  border-radius: 5px;
  margin-top: 10px;
}

.cascading-right {
  margin-right: 0px;
}

@media (max-width: 991.98px) {
  .cascading-right {
    margin-right: 0;
  }
}

.tentaikhoan{
  margin: auto;
  width: 350px;
}
.nhapemail{
  margin: auto;
  width: 350px;
}
.nhapmk{
  margin: auto;
  width: 350px;
}
.btn-sign{
  width: 130px;
  background-color: #2E1C11;
  color: white;
  height: 40px;
  border-radius: 20px;
  margin-left: 270px;
}
.btn-sign:hover{
  background-color: #708090;
  color: white;
  height: 40px;
  border-radius: 20px;
  font-weight: 600;
}
.dangnhap:hover{
  color: rgb(165, 71, 165);
  font-size: 17px;
}
.dangnhap{
  color: rgb(109, 47, 109);
  font-size: 17px;
}
</style>
