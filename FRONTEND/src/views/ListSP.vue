<script>
import ListUser from "../components/ListUser.vue";
import UserService from "../services/User.service";
import toastsVue from "../components/toasts.vue";
import ProductService from "../services/Product.service";
import ListProduct from "../components/ListProduct.vue";
import Productcard from "../components/Productcard.vue";
import Usercard from "../components/Usercard.vue";
import toast from "../assets/js/toasts";
export default {
    data() {
        return {
            users: [],
            products: [],
            activeIndex: -1,
            activeUser: -1,
            toasts: {
                title: "Warning",
                msg: "Bạn không phải ADMIN",
                type: "warn",
                duration: 3000
            },
        }
    },
    computed: {
        getindex() {
            if (this.activeIndex != -1) {
                const list = document.querySelectorAll(".product-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeIndex].classList.add("active");
                return this.products[this.activeIndex];
            }
        },
        getindexuser() {
            if (this.activeUser != -1) {
                const list = document.querySelectorAll(".user-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeUser].classList.add("active");
                return this.users[this.activeUser];
            }
        }
    },
    components: {
        ListUser,
        ListProduct,
        toastsVue,
        Productcard,
        Usercard
    },
    methods: {
        toast,
        async getall() {
            try {
                this.products = await ProductService.getAll();
                this.users = await UserService.getAll();
            } catch (error) {
                console.log(error);
                this.toast();
                setTimeout(() => {
                    this.$router.push({ name: "ShopMain" });
                }, 1000);
            }
        },
    },
    created() {
        this.getall();
    },
}
</script>

<template>
    <div>
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
                    <a class="navbar-brand" href="">
                        <router-link to="/ListOrder" class="text">QUẢN LÝ ĐƠN HÀNG</router-link>
                    </a>
                    <router-link to="/"> <img src="../assets/img/LGA.png"
                            style=" margin-left: 220px; width: 150px; height: 50px; margin-top: -6px;" alt="">
                    </router-link>
                </nav>
            </div>

        </div>
    </div>

    <div style="background-color: #fafafa;">
        <div style="padding-top: 10px;">
            <div style="margin-left: 480px;">
                <h4 class="titleh4">QUẢN LÝ SẢN PHẨM</h4>
            </div>
            <div>
                <router-link to="/addproduct">
                    <button class="btn btn-success" style="margin-left: 1100px; margin-top: -85px;">
                        Thêm Sản phẩm</button>
                </router-link>
            </div>
        </div>

        <div class="background">
            <div class="d-flex">
                <div>
                    <div
                        style="background-color: #ccc; border-top-left-radius: 10px; border-top-right-radius: 10px; min-width: 1090px;">

                        <div style="padding-left: 20px; padding-top: 10px; min-width: 1080px;">
                            <ul class="list-group">
                                <table class="mb-2">
                                    <tr class="row">
                                        <th class="col-4" scope="col">Tên sản phẩm</th>
                                        <th class="col-2" style="padding-left: 0px;" scope="col">Giá</th>
                                        <th class="col-2" style="padding-left: 10px;" scope="col">Khối lượng</th>

                                        <th class="col-3" style="padding-left: 0px;" scope="col">Màu sắc</th>
                                        <th class="col-1" style="padding-left: 0px;" scope="col">Xóa</th>

                                    </tr>
                                </table>
                            </ul>
                        </div>

                    </div>
                    <div id="product">
                        <ListProduct :products="products" :refeshlist="getall" :getindex="getindex"
                            v-model:activeIndex="activeIndex"></ListProduct>

                    </div>
                </div>

                <div class="card_product border border-light border-2 h-100 bg-light text-dark" style="padding-left: 5px;"
                    v-if="getindex">
                    <div style="border: 2px solid #ccc; border-radius: 5px; padding: 10px 5px 15px;">
                        <h6 style="border-bottom: 2px solid #2e1c11;">Chỉnh sửa sản phẩm</h6>

                        <Productcard :products="getindex"></Productcard>
                        <router-link :to="{
                            name: 'editproduct',
                            params: { id: getindex._id },}">
                            <span class="badge bg-success" style="font-size: 16px; margin-top: 10px; color: #fafafa;">
                                <i class="bi bi-pencil-square"></i> Chỉnh sửa
                            </span>
                        </router-link>
                    </div>
                </div>
            </div>
            <br>

        </div>
    </div>
    <toastsVue></toastsVue>
</template>
<style scoped>
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

.background {
    border-radius: 10px;
    margin-top: -17px;
}
</style>