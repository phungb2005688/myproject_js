<script>
import HeaderShopVue from "../components/HeaderShop.vue";
import ListOrder from "../components/ListOrd.vue";
import UserService from "../services/User.service";
import toastsVue from "../components/toasts.vue";
import ProductService from "../services/Product.service";
import ListProduct from "../components/ListProduct.vue";
import Productcard from "../components/Productcard.vue";
import Usercard from "../components/Usercard.vue";
import toast from "../assets/js/toasts";
import OrderService from "../services/Order.service";

export default {
    data() {
        return {
            orders: [],
            products: [],
            activeOrder: -1,
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
        getindexorder() {
            if (this.activeOrder != -1) {
                const list = document.querySelectorAll(".order-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeOrder].classList.add("active");
                return this.orders[this.activeOrder];
            }
        },
        getindexuser() {
            if (this.activeUser != -1) {
                const list = document.querySelectorAll(".order-item");
                list.forEach(element => {
                    element.classList.remove("active");
                });
                list[this.activeUser].classList.add("active");
                return this.orders[this.activeUser];
            }
        }
    },
    components: {
        HeaderShopVue,
        ListOrder,
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
                this.orders = await OrderService.getAll();
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

        <div style="padding-top: 10px; ">
            <div style="margin-left: 480px;">
                <h4 class="titleh4">QUẢN LÝ ĐƠN HÀNG</h4>

            </div>
            <div class="row" style="width: 1200px;">
                <div class="col-7" style="margin-right: 100px;">
                    <ListOrder :orders="orders" :refeshlist="getall" v-model:activeOrder="activeOrder"></ListOrder>

                </div>
                <!-- <div class="col-4" style="margin-left: 50px; width: 300px; min-height: 350px; padding-right: 20px;">
                    <div class="list_item_user" id="user">
                        <div class="card_product border border-light border-2 h-100 text-dark"
                            style="padding: 10px; background-color: #c3e0ff;" v-if="getindexuser">
                            <div style="text-align: center;">
                                <i style=" width: 55px; height: 50px; background-color: #fff; font-size: 30px; border-radius: 40px; padding-top: 8px;"
                                    class="fa-solid fa-user-check"></i>
                                <Usercard :users="getindexuser" v-model:activeUser="activeUser"></Usercard>
                            </div>
                        </div>
                    </div>
                </div> -->
            </div>
        </div>
    </div>
    <br>
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

.list_item_user {
    /* margin-top: -190px; */
    padding-left: 10px;
}
</style>