<script>
import ProductService from "../services/Product.service";
import toastjs from "../assets/js/toasts";
export default {
    data() {
        return {
            toasts: {
                title: "",
                msg: "",
                type: "",
                duration: 0
            },
        }
    },
    props: {
        products: Array,
        refeshlist: Function,
        activeIndex: { type: Number, default: -1 },
    },
    emits: ["update:activeIndex"],
    methods: {
        toastjs,
        async delproduct(id) {
            try {
                await ProductService.delete(id);
                this.refeshlist();
                this.toasts.title = "Success",
                    this.toasts.msg = "Đã xóa sản phẩm",
                    this.toasts.type = "success",
                    this.toasts.duration = 2000
                this.toastjs();
            } catch (error) {
                console.log(error);
                this.toasts.title = "Warning",
                    this.toasts.msg = "Bạn chưa đăng nhập hoặc bạn không phải ADMIN",
                    this.toasts.type = "warn",
                    this.toasts.duration = 2000
                this.toastjs();
            }
        },
        updateActiveIndex(index) {
            this.$emit("update:activeIndex", index);
        },
    }
}
</script>
<template>
    <div style="width: 1080px;">
        <ul class="list-group">

            <li class="row list-group-item product-item d-flex justify-content-between" v-for="(product, index) in products"
                :key="product._id" @click="updateActiveIndex(index)">

                <span class="col-4">{{ product.title }}</span>
                <span class="col-2" style="padding-left: 7px;">{{ product.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }}</span>
                <span class="col-2" style="padding-left: 43px;">{{ product.size }}g</span>
                <span class="col-3" style="padding-left: 35px;">{{ product.color }}</span>

                <div class=" col-1 fa-solid fa-trash" style="padding-left: 35px; color: rgb(249, 135, 135);"
                    @click="delproduct(product._id)"> 
                </div>
            </li>
        </ul>
    </div>
</template>
<style scoped>
.list-group-item:hover {
    background-color: #E4F1FF;
    color: black;
}

.list-group-item.active {
    z-index: 2;
    color: #000;
    background-color: #E4F1FF;
    border-color: #E4F1FF;
}
</style>