<script>
import HeaderShopVue from "../components/HeaderShop.vue";
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
        HeaderShopVue,
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
                }, 5000);
            }
        },
    },
    created() {
        this.getall();
    },
}
</script>

<template>
    <div style="padding-bottom: 10px;">
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

    <div style="margin-top: 10px;">
        <div class="background">
            <div style="padding-top: 30px;">
                <h1 class="welcome">CHÀO MỪNG ĐẾN VỚI FALLING & KMD</h1>

            </div>
        </div>
    </div>
</template>
<style scoped>
.background {
    background-image: url(https://fluxandstone.com/cdn/shop/products/DropPearl-GoldFill-White-Large_1200x600_crop_center.jpg?v=1621290247);
    width: 1263px;
    height: 480px;
    margin-top: -13px;
}

.welcome {
    text-align: center;
    border: 2px dashed #000;
    border-radius: 10px;
    width: 900px;
    margin: auto;
    padding: 10px;
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
    background-color: #fbf9f9;
    padding: 17px;
    font-size: 17px;
}
</style>