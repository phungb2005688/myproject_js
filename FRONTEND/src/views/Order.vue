<script>
import { mapState } from "pinia";
import { useAuthStore } from "../stores/Auth.store";
import HeaderShop from '@/components/HeaderShop.vue';
import FooterShop from '@/components/FooterShop.vue';
import CartService from '../services/Cart.service';
import toastsVue from '../components/toasts.vue';
import toastsjs from '../assets/js/toasts.js'
import CartItem from "../components/CartItem.vue";
import OrderService from '../services/Order.service';
export default {
    data() {
        return {
            carts: [],
            toasts: {
                title: "",
                msg: "",
                type: "",
                duration: 0
            },
        }
    },
    components: {
        HeaderShop,
        toastsVue,
        CartItem,
        FooterShop,
    },
    computed: {
        ...mapState(useAuthStore, {
            currentUser: "user",
        }),
    },
    methods: {
        getiduser() {
            const user = JSON.parse(localStorage.getItem("user"));
            return user._id;
        },
        async handelbuttonaddorder() {
            for (let item of this.carts) {
                let order = {
                    userId: item.userId,
                    productId: item._id,
                    quantity: item.quantity,
                    address: "Lấy tại shop",
                    status: "Chờ xác nhận",
                };
                await OrderService.create(order);
            }
        },
        async getcarts() {
            try {
                this.carts = await CartService.get(this.getiduser());
            } catch (error) {
                console.log(error);
            }
        },
        async delcart(index) {
            // this.toasts.title = "Deleted",
            // this.toasts.msg = "XÓA SẢN PHẨM THÀNH CÔNG",
            // this.toasts.type = "error",
            // this.toasts.duration = 2000
            // this.toastsjs();
            await CartService.delete(this.carts[index]._id)
            this.refeshlistcart();
        },
        toastsjs,
        refeshlistcart() {
            this.getcarts();
        },
        registerproduct() {
            if (this.carts.length > 0) {

                this.toasts.msg = "THANH TOÁN THÀNH CÔNG",
                    this.toasts.type = "success",
                    this.toasts.duration = 2000,
                    this.toastsjs();
            } else {
                this.toasts.title = "Failed",
                    this.toasts.msg = "Bạn chưa có sản phẩm",
                    this.toasts.type = "error",
                    this.toasts.duration = 2000,
                    this.toastsjs();
            }
        },
        total() {
            var total = 0;
            for (var i in this.carts) {
                total += (this.carts[i].price * this.carts[i].quantity);
            }
            return total;
        }
    },
    created() {
        this.refeshlistcart();
    },
}
</script>

<template>
    <HeaderShop></HeaderShop>
    <toastsVue></toastsVue>

    <section class="mb-5">
        <div class="container">

            <div style="padding-top: 5px; margin-left: 400px;">
                <h3 class="chitiet">CHI TIẾT ĐẶT HÀNG</h3>
            </div>

            <div class=" h-200">
                <div class="row">

                    <div class="col-md-6">
                        <hr style="width: 550px; margin-top: 25px; border: 1px solid #3e3e3e;">

                        <CartItem :refeshlistcart="refeshlistcart" :carts="carts" @deleted:cartIndex="delcart"></CartItem>
                    </div>

                    <div class="col-lg-5" style="margin-top: 12px; margin-left: 90px;">
                        <div style="border: 1px solid #2e1c11; width: 280px; margin-top: 10px; padding: 5px; border-radius: 10px; margin-bottom: 5px         ;">
                            <h6 style="padding-left: 5px; padding-top: 5px;">Tổng sản phẩm khách hàng mua: {{ carts.length }}
                            </h6>
                        </div>
                        <span style=" font-weight: 600; color: #2e1c11; border-bottom: 2px solid #2e1c11;">Thanh toán trực
                            tuyến</span>
                        <div class="card">
                            <div class="accordion" id="accordionExample">
                                <div class="card">
                                    <div class="card-header p-0" id="headingTwo">
                                        <h2 class="mb-0">
                                            <button style="width: 448px;"
                                                class="btn btn-light text-left collapsed p-3 rounded-0 border-bottom-custom"
                                                type="button">
                                                <div class="d-flex align-items-center justify-content-between">
                                                    <span style="margin-right: 0px;">Paypal</span>
                                                    <img src="https://i.imgur.com/7kQEsHU.png" width="30">
                                                </div>
                                            </button>
                                        </h2>
                                    </div>
                                    <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo"
                                        data-parent="#accordionExample">
                                        <div class="card-body">
                                            <input type="text" class="form-control" placeholder="Paypal email">
                                        </div>
                                    </div>
                                </div>

                                <div class="card">

                                    <div id="collapseOne" class="collapse show" aria-labelledby="headingOne"
                                        data-parent="#accordionExample">
                                        <div class="card-body payment-card-body">
                                            <span class="font-weight-normal card-text">Địa chỉ nhận hàng</span>

                                            <div class="diachi">
                                                <div
                                                    style="border: 1px solid #ccc; height: 35px; border-radius: 5px; padding-top: 5px;">
                                                    <i class="fa-solid fa-location-dot"></i>
                                                    <span style="padding-left: 50px; font-weight: 500;">Lấy tại shop</span>
                                                </div>
                                            </div>
                                            <div class="row mt-3 mb-3">

                                                <div class="col-md-6">
                                                    <span class="font-weight-normal card-text">Số điện thoại </span>
                                                    <div class="input1">
                                                        <i class="fa-solid fa-phone"></i>
                                                        <input type="text" class="form-control" placeholder="Số điện thoại">
                                                    </div>
                                                </div>

                                                <div class="col-md-6">
                                                    <span class="font-weight-normal card-text">Vận chuyển</span>
                                                    <div class="input1">
                                                        <div
                                                            style="border: 1px solid #ccc; height: 35px; border-radius: 5px; padding-top: 5px;">
                                                            <i class="fa-solid fa-truck-fast"></i>
                                                            <span style="padding-left: 50px; font-weight: 500;">Miễn
                                                                phí</span>

                                                        </div>
                                                    </div>
                                                </div>

                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div>
                            <div class="pt-3" style="margin-left: 190px;">
                                <h5 style="margin-left: 35px;">TỔNG TIỀN: {{
                                    total().toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }}
                                    đ
                                </h5>

                                <div class="text-align-center">
                                    <div class="d-flex justify-content-between mb-5">
                                        <button class="btn thanhtoan" @click="handelbuttonaddorder()">
                                            <router-link to="/thank" class="text-white text-decoration-none">XÁC NHẬN ĐẶT
                                                HÀNG<i class="fa-solid fa-arrow-right"
                                                    style="padding-left: 10px;"></i></router-link>
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div>
                        <div class="text-align-center">
                            <div class="d-flex justify-content-between mb-5">
                                <button class="btn thanhtoan1">
                                    <i class="fa-solid fa-arrow-left" style="margin-right: 5px; color: ;"></i>
                                    <router-link to="/" class="tieptuc"> Tiếp tục mua sắm
                                    </router-link>
                                </button>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>
</template>
<style scoped>
.chitiet {
    text-align: center;
    color: #fff;
    margin-top: 10px;
    border: 1px solid #2e1c11;
    background-color: #2e1c11;
    width: 330px;
    padding: 5px;
    border-radius: 10px;
}

.container {
    margin-top: 10px;
}

.btn-light {
    color: #212529;
    width: 140px;
}

.btn-light1 {
    color: #212529;
    width: 140px;
}

.btn-light2 {
    color: #212529;
    width: 133px;
}

.btn-light:hover {
    color: #212529;
    background-color: #e2e6ea;
    width: 140px;
}

.btn-light1:hover {
    color: #212529;
    background-color: #e2e6ea;
    width: 140px;
}

.btn-light2:hover {
    color: #212529;
    background-color: #e2e6ea;
    width: 133px;
    /* margin: auto; */
}

.input1 {
    position: relative;
    margin-top: 5px;
}

.input1 i {
    position: absolute;
    top: 11px;
    left: 11px;
    color: #989898;
}

.input1 input {
    text-indent: 25px;
}

.diachi {
    position: relative;
    margin-top: 5px;
    margin-left: 10px;
}

.diachi i {
    position: absolute;
    top: 11px;
    left: 11px;
    color: #989898;
}


.thanhtoan {
    background-color: #949494;
    color: white;
    margin-left: 95px;
    margin-top: 10px;
}

.thanhtoan:hover {
    background-color: #2e1c11;
    color: white;
    font-weight: 600;
}

.thanhtoan1 {
    background-color: antiquewhite;
    color: #2e1c11;
    margin-left: 0px;
    margin-top: 10px;
}

.thanhtoan1:hover {
    background-color: #2e1c11;
    color: white;
    font-weight: 600;
}

.tieptuc {
    color: #2e1c11;
    text-decoration: none;
}

.tieptuc:hover {
    color: white;
    text-decoration: none;
}

@media (min-width: 1025px) {
    .h-custom {
        height: 100%;
    }
}

.card-registration .select-input.form-control[readonly]:not([disabled]) {
    font-size: 1rem;
    line-height: 2.15;
    padding-left: .75em;
    padding-right: .75em;
}

.card-registration .select-arrow {
    top: 13px;
}

.bg-grey {
    background-color: #ffffff;
}

@media (min-width: 992px) {
    .card-registration-2 .bg-grey {
        border-top-right-radius: 16px;
        border-bottom-right-radius: 16px;
    }
}

@media (max-width: 991px) {
    .card-registration-2 .bg-grey {
        border-bottom-left-radius: 16px;
        border-bottom-right-radius: 16px;
    }
}
</style>