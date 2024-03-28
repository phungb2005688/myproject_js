<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";
export default {
  props: {
    product: { type: Object, required: true },
    resetAfterSubmit: { type: Boolean, default: false },
  }
  ,
  data() {
    const productform = yup.object().shape({
      name: yup
        .string()
        .required("Bạn chưa nhập Tên sản phẩm.")
        .min(7, "Tên phải có ít nhất 7 ký tự."),
      img: yup
        .string()
        .required("Sản phẩm phải có Hình ảnh."),
      price: yup
        .string()
        .required("Bạn chưa nhập giá sản phẩm."),
      description: yup
        .string()
        .required("Bạn chưa nhập Mô tả cho sản phẩm.")
        .min(10, "Mô tả sản phẩm phải ít nhất 10 ký tự."),
      category: yup
        .string()
        .required("Bạn chưa nhập Loại của sản phẩm."),
      size: yup
        .string()
        .required("Bạn chưa nhập Khối lượng của sản phẩm."),
      color: yup
        .string()
        .required("Bạn chưa nhập Màu cho sản phẩm."),
    });
    return {
      productLocal: this.product,
      productform,
    }
  },
  components: {
    Form,
    Field,
    ErrorMessage
  },
  emits: ['submit:product'],
  methods: {
    addImge() {
      document.querySelector("#imgproduct2").style.display = "block";
    },
    submitproduct() {
      this.$emit('submit:product', this.productLocal);
      if (this.resetAfterSubmit) {
        this.$refs.contactForm.resetForm();
      }
    },
  }
}
</script>
<template>
  <div class="wrapper">
    <Form :validation-schema="productform" @submit="submitproduct">
      <div class="form-outline">
        <div class="tensanpham">
          <div class="sanpham">
            <label for="nameproduct">Tên sản phẩm:</label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="nameproduct" name="name" placeholder="Nhập tên sản phẩm"
              v-model="productLocal.title" />
            <ErrorMessage name="name" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="hinhanh">
          <div class="hinhanh1">
            <label for="imgproduct">Hình ảnh:</label>
          </div>
          <div>
            <div style="display: flex; flex-direction: row; width: 600px;">
              <Field type="text" class="form-control" id="imgproduct" name="img"
                placeholder="Nhập đường dẫn hình ảnh sản phẩm" v-model="productLocal.img[0]" />
              <i class="bi bi-file-plus btn_img-add" @click="addImge()"></i>
            </div>
            <input type="text" class="nhapvao form-control" id="imgproduct2" name="img"
              style="display:none; margin: 10px 0;" v-model="productLocal.img[1]">
            <ErrorMessage name="img" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="tensanpham">
          <div class="gia">
            <label for="priceproduct">Giá sản phẩm: </label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="priceproduct" name="price" placeholder="Nhập giá sản phẩm"
              v-model="productLocal.price" />
            <ErrorMessage name="price" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="tensanpham">
          <div class="mota">
            <label for="priceproduct">Mô tả: </label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="nameproduct" name="description"
              placeholder="Nhập mô tả sản phẩm" v-model="productLocal.desc" />
            <ErrorMessage name="description" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="tensanpham">
          <div class="loai">
            <label for="priceproduct">Loại: </label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="categoryproduct" name="category"
              placeholder="Nhập loại sản phẩm" v-model="productLocal.categories" />
            <ErrorMessage name="category" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="tensanpham">
          <div class="weight">
            <label for="priceproduct">Khối lượng: </label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="sizeproduct" placeholder="Nhập khối lượng sản phẩm"
              name="size" v-model="productLocal.size" />
            <ErrorMessage name="size" class="text-danger" />
          </div>
        </div>
      </div>

      <div class="form-outline">
        <div class="tensanpham">
          <div class="loai">
            <label for="priceproduct">Màu: </label>
          </div>
          <div>
            <Field type="text" class="nhapvao form-control" id="colorproduct" name="color" placeholder="Nhập màu sản phẩm"
              v-model="productLocal.color" />
            <ErrorMessage name="color" class="text-danger" />
          </div>
        </div>
      </div>

      <div style="margin: 20px 0px 0px 290px;">
        <button type="submit" class="btn btn-success">Cập nhật<i class="fa-solid fa-check" style="padding-left: 5px;"></i></button>
        <router-link to="/ListSP" style="margin: 10px;">
          <button class="btn undo">Trở về <i class="fa-solid fa-rotate-left" style="padding-left: 5px;"></i></button>
        </router-link>
      </div>

      <br>
    </Form>
  </div>
</template>
<style scoped>
.undo{
  background-color: #ccc;
  color: #000;
}
.undo:hover{
  background-color: #2E1C11;
  color: white;
}
.nhapvao {
  margin-top: 15px;
  min-width: 600px;
  height: 40px;
}

.tensanpham {
  margin-top: 10px;
  display: flex;
}

.sanpham {
  margin-top: 20px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  color: #2E1C11;
}

.hinhanh {
  margin-top: 25px;
  display: flex;
}

.hinhanh1 {
  margin-top: 7px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  padding-right: 37px;
  color: #2E1C11;
}

.mota {
  margin-top: 20px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  padding-right: 63px;
  color: #2E1C11;
}

.gia {
  margin-top: 18px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  padding-right: 3px;
  color: #2E1C11;
}

.loai {
  margin-top: 18px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  padding-right: 76px;
  color: #2E1C11;
}

.weight {
  margin-top: 18px;
  margin-right: 15px;
  font-size: 17px;
  font-weight: 600;
  padding-right: 24px;
  color: #2E1C11;
}

.wrapper {
  margin: 10px 100px 0px 280px;
}

.btn_img-add {
  font-size: 30px;
  color: rgb(0, 0, 0);
}</style>