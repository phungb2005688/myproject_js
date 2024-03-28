<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
import UserService from "../services/User.service";
import toast from "../assets/js/toasts";
import { mapActions } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
export default {
  props: { user: Object },
  data() {
    const userform = yup.object().shape({
      name: yup
        .string()
        .required("Bạn chưa nhập Tên người dùng.")
        .min(4, "Tên phải ít nhất 4 ký tự."),
      email: yup
        .string()
        .required("Bạn chưa nhập Email.")
        .email("Email không hợp lệ"),
      pwd: yup
        .string()
        .required("Bạn chưa nhập Mật khẩu.")
    });
    return {
      userform,
      infouser: this.user,
      toasts: {
        title: "",
        msg: "",
        type: "",
        duration: 0
      },
    }
  },
  components: {
    Form,
    Field,
    ErrorMessage
  },
  methods: {
    toast,
    ...mapActions(useAuthStore, ["logout"]),
    async updateUser() {
      try {
        await UserService.update(this.infouser._id, this.infouser);
        this.toasts.title = "Success",
          this.toasts.msg = "Đã sửa thông tin vui lòng đăng nhập lại !",
          this.toasts.type = "success",
          this.toasts.duration = 3000
        this.toast();
        setTimeout(() => {
          this.logout();
          this.$router.push({ name: "login" });
        }, 2000);
      } catch (error) {
        this.toasts.title = "Faild",
          this.toasts.msg = "Có lỗi hoặc trùng tên người dùng",
          this.toasts.type = "error",
          this.toasts.duration = 3000
        this.toast();
        console.log(error);
      }
    },
  },
}
</script>
<template>
  <div>
    <Form :validation-schema="userform">
      <div class="imageChim1">
        <header>
          <h3 style="text-align: center; font-weight: 600; padding-top: 15px;">
            CẬP NHẬT THÔNG TIN 
          </h3>
        </header>
        <div class="form-group edit-user">
          <label for="nameproduct" class="ten">Tên tài khoản:</label>
          <Field type="text" class="form-control" id="nameproduct" name="name" v-model="infouser.username"
            placeholder="Enter name product" style="width: 300px; margin-left: 40px;"/>
          <ErrorMessage name="name" class="text-danger" />
        </div>
        <div class="form-group edit-user">
          <label for="nameproduct" class="ten">Email:</label>
          <Field type="text" class="form-control" id="nameproduct" name="email" v-model="infouser.email"
            placeholder="Enter name product" style="width: 300px; margin-left: 40px;"/>
          <ErrorMessage name="email" class="text-danger" />
        </div>
        <button type="submit" style="margin-left: 200px; margin-top: 10px;" class="btn btn-success" @click="updateUser">Cập Nhật</button>
        <br>
      </div>

    </Form>
  </div>
</template>
<style>
.edit-user {
  margin-left: 50px;
}

.imageChim1 {
  background-image: url(https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQDwkMYGdjGfSo_12Ko97WM8tgByu_3UgnuA9LJsgWBYYEGEdzW1qSa-fl9Qe376i44tVY&usqp=CAU);
  border-radius: 20px;
  height: 240px;
  margin-left: 70px;
  width: 500px;
}
.ten{
  margin-left: 40px;
  font-weight: 600;
}
</style>