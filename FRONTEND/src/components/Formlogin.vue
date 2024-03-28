<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import { mapActions } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import toast from "../assets/js/toasts";
export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const Loginform = yup.object().shape({
      username: yup
        .string()
        .required("Bạn chưa nhập Tên người dùng.")
        .min(4, "Tên phải ít nhất 4 ký tự."),
      password: yup
        .string()
        .required("Bạn chưa nhập Mật khẩu.")
    });
    return {
      Loginform,
      toasts: {
        title: "Warning",
        msg: "Tên đăng nhập hoặc mật khẩu không đúng!",
        type: "warn",
        duration: 2000
      },
    }
  },
  methods: {
    toast,
    showPwd() {
      if (document.querySelector("#checkpwd").checked == true) {
        document.querySelector("#pwd").type = 'text';
      } else {
        document.querySelector("#pwd").type = 'password';
      }
    },
    ...mapActions(useAuthStore, ["login"]),
    async handleLogin(user) {
      try {
        await this.login(user);
        location.href = 'http://localhost:8001/';
      } catch (error) {
        this.toast();
        console.log(error);
      }
    },
  },
};
</script>
<template>
  <Form :validation-schema="Loginform" @submit="handleLogin">
    <!--========== Email input============== -->
    <div class="form-outline">
      <div class="tennguoidung">
        <div class="nguoidung">
          <label class="form-label" for="username">Tên người dùng</label>
        </div>
        <div class="">
          <Field id="name" placeholder="Nhập tên tài khoản" name="username" type="text"
            class="nhapvao form-control form-control " />
          <ErrorMessage name="username" class="text-danger" />
        </div>
      </div>
    </div>

    <!--========== Password input============== -->
    <div class="form-outline mb-4">
      <div class="nhapmatkhau">
        <div class="matkhau">
          <label class="form-label" for="pwd">Mật khẩu</label>
        </div>
        <div class="">
          <Field id="pwd" placeholder="Nhập mật khẩu" name="password" type="password"
            class="nhapvao form-control form-control" />
          <ErrorMessage name="password" class="text-danger" />
        </div>
      </div>
    </div>

    <div class="d-flex justify-content-between align-items-center">
      <!-- Checkbox -->
      <div class="tich form-check mb-0">
        <input class=" form-check-input me-2 dautich" type="checkbox" value="" id="checkpwd" @click="showPwd()" />
        <label class="hienmk form-check-label" for="checkpwd">
          Hiện mật khẩu
        </label>
      </div>
    </div>
    <div class="text-center tex t-lg-start mt-4 pt-2">
      <button class="btn btn-login" style="padding-left: 2.5rem; padding-right: 2.5rem;">Đăng Nhập</button>
      <p class="small fw-bold mt-2 pt-1 mb-0" style="color: #2E1C11;">Bạn chưa có tài khoản? 
        <router-link to="/logup" class="dangky">Đăng Ký</router-link>
          
      </p>
    </div>
  </Form>
</template>
<style>
.nhapvao {
  margin-top: 15px;
  width: 400px;
  height: 40px;
}

.tennguoidung {
  margin-top: 10px;
  display: flex;
  padding-left: 280px;
}

.nhapmatkhau {
  margin-top: 30px;
  display: flex;
  padding-left: 280px;
}

.nguoidung {
  margin-top: 20px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
}

.matkhau {
  margin-top: 20px;
  margin-right: 62px;
  font-size: 17px;
  font-weight: 600;
}

.tich {
  margin-left: 415px;
}
.form-check-input:checked {
    background-color: #2E1C11;
    border-color: #2E1C11;
}
.hienmk {
  color: #2E1C11;
  font-weight: 600;
}

.btn-login{
  background-color: #2E1C11;
  color: white;
  height: 40px;
  border-radius: 20px;
}
.btn-login:hover{
  background-color: #708090;
  color: white;
  height: 40px;
  border-radius: 20px;
  font-weight: 600;
}
.dangky:hover{
  color: rgb(165, 71, 165);
  font-size: 17px;
}
.dangky{
  color: rgb(109, 47, 109);
  font-size: 17px;
}
</style>