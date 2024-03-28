<script>
import HeaderShop from '@/components/HeaderShop.vue'
import ProductService from '../services/Product.service'
import CartService from '../services/Cart.service'
import toastsVue from '../components/toasts.vue'
import toastsjs from '../assets/js/toasts.js'
import { mapState } from 'pinia'
import { useAuthStore } from "@/stores/Auth.store";
export default {
    data() {
        return {
            detailproduct: [],
            cartitem: {
                userId: '',
                productId: this.$route.params.id,
                quantity: 1,
                title: "",
                img: "",
                price: "",
                size: "",
                color: "",
            },
            carts: [],
            toasts: {
                // title: "THÊM VÀO GIỎ HÀNG THÀNH CÔNG",
                // msg: "+1 sp",
                // type: "success",
                // duration: 2000
            },
            sub_quantity: 1,
        }
    },
    computed: {
        ...mapState(useAuthStore, {
            currentUser: "user",
        }),
    },
    components: {
        HeaderShop,
        toastsVue
    },
    methods: {
        toastsjs,
        async getproduct() {
            try {
                this.detailproduct = await ProductService.get(this.$route.params.id);
                this.cartitem.title = this.detailproduct.title;
                this.cartitem.img = this.detailproduct.img[0];
                this.cartitem.price = this.detailproduct.price;
                this.cartitem.size = this.detailproduct.size;
                this.cartitem.color = this.detailproduct.color;
            } catch (error) {
                console.log(error);
            }
        },
        async getidcart() {
            this.cartitem.quantity = this.sub_quantity;
            var exitcart = false;

            try {
                this.carts = await CartService.get(this.currentUser._id);
                this.cartitem.userId = this.currentUser._id;
                this.carts.map((cartproduct) => {
                    if (cartproduct.productId == this.cartitem.productId) {
                        this.cartitem.quantity += cartproduct.quantity;
                        CartService.update(cartproduct._id, this.cartitem);
                        exitcart = true;
                        this.toastsjs();
                        setTimeout(() => {
                            this.$router.push({ name: 'CartShop' });
                        }, 1000);
                    }
                })
                if (exitcart === false) {
                    this.cartitem.userId = this.currentUser._id;
                    CartService.create(this.cartitem);
                    this.toastsjs();
                    setTimeout(() => {
                        this.$router.push({ name: 'CartShop' });
                    }, 1000);
                }
            } catch (error) {
                // this.toasts.title = "Message",
                this.toasts.msg = "ĐĂNG NHẬP ĐỂ MUA HÀNG",
                    this.toasts.type = "warn",
                    this.toasts.duration = 3000,
                    this.toastsjs();
                console.log(error);
            }
        },
    },
    created() {
        this.getproduct();
    },

}
</script>
<template>
    <HeaderShop></HeaderShop>

    <toastsVue></toastsVue>
    <div class="container">
        <div style="padding-top: 5px; margin-left: 400px;">
            <h3 class="chitiet">CHI TIẾT SẢN PHẨM</h3>
        </div>
    </div>

    <div class="wrapper">

        <div class="details d-flex justify-content-between">
            <div class="img_product">
                <div id="carouselExampleControls" data-bs-ride="carousel">
                    <div>
                        <div v-for="(img, index) in detailproduct.img" :class="{ active: index == 0 }">
                            <img :src="img" class="" style="width: 320px; " alt="...">
                        </div>
                    </div>
                </div>
            </div>
            <div class="info_product " style="margin-left: 100px;">
                <h3 style="font-weight: 600;">{{ detailproduct.title }}</h3>
                <div style="margin-top: ;">
                    <i class="fa-solid fa-star star"></i>
                    <i class="fa-solid fa-star star"></i>
                    <i class="fa-solid fa-star star"></i>
                    <i class="fa-solid fa-star star"></i>
                    <i class="fa-solid fa-star star"></i>
                </div>
                <div class="borderprice">
                    <h5>Giá: {{ detailproduct.price.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".") }} đ</h5>

                    <div class="quatitly_product">
                        <h6 style="margin-right: 10px; margin-top: 7px;">Số lượng: </h6>
                        <input id="quantity" name="quantity" type="number" v-model="sub_quantity"
                            class="form-control form-control-sm soluong" />
                    </div>
                </div>

                <p style="margin-top: 20px;">
                    <span class="mota">CHI TIẾT SẢN PHẨM: </span>
                    <span style="padding-left: 10px;">{{ detailproduct.desc }}</span>
                </p>
                <div class="color_product">
                    <h6>Màu sắc: {{ detailproduct.color }} </h6>

                </div>
                <div class="weight_product">
                    <h6>Khối lượng: {{ detailproduct.size }}g</h6>

                </div>

                <div class="btn_product">
                    <router-link to="/">
                        <button type="button" class="btn back" style="width:130px; margin-right: 400px;">
                            <i class="fa-solid fa-arrow-left" style="margin-right: 10px;"></i>Trang chủ
                        </button>
                    </router-link>
                    <button type="submit" class="btn order" style="width:130px; float: left;" @click="getidcart()">
                       Đặt hàng <i class="fa-solid fa-arrow-right" style="margin-left: 10px;"></i>
                    </button>
                        
                </div>

            </div>

        </div>
    </div>
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

.mota {
    border-bottom: 1px solid #2e1c11;
}

.borderprice {
    width: 630px;
    border: 1px solid #efefef;
    border-radius: 5px;
    background-color: #efefef;
    padding: 15px;
    margin-top: 10px;
}

.btn_product {
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
    margin-bottom: 50px;
}

.weight_product,
.color_product {
    display: flex;
    flex-direction: column;
    max-width: 400px;
    color: #2e1c11;
}

.quatitly_product {
    display: flex;
    width: 150px;
    margin-top: 15px;
}

.star {
    padding-left: 2px;
}

.soluong {
    width: 50px;
    border: none;
    height: 20px;
    font-size: 16px;
}

.back {
    background-color: antiquewhite;
    color: #2e1c11;
    border: 1px solid antiquewhite;
}

.back:hover {
    background-color: #2e1c11;
    color: white;
    border: 1px solid #2e1c11;
    font-weight: 600;
}

.order {
    background-color: rgb(221, 221, 221);
    color: #2e1c11;
    border: 1px solid antiquewhite;
}

.order:hover {
    background-color: #2e1c11;
    color: white;
    border: 1px solid #2e1c11;
    font-weight: 600;
}
.list_btn_size,
.list_btn_color {
    margin: 0 10px;
    display: flex;
    flex-wrap: wrap;
}

.list_btn_size button,
.list_btn_color button {
    margin: 10px 5px;
}

/* .btn {
    width: 100px;
} */

.wrapper {
    margin: 30px 100px;
    min-height: 300px;
}

.heading {
    margin: 0 100px;
}

.title {
    display: flex;
    justify-content: center;
    flex-direction: column;
    width: 100%;
    height: 100px;
}</style>