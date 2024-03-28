<script>
import OrderService from "../services/Order.service";
import toastsVue from "./toasts.vue";
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
    components: {
        toastsVue
    },
    props: {
        orders: Array,
        refeshlist: Function,
        activeUser: { type: Number, default: -1 },
    },
    emits: ['update:activeOrder'],
    methods: {
        toastjs,
        async delorder(id) {
            try {
                await OrderService.delete(id);
                this.refeshlist();
                this.toasts.title = "Success",
                    this.toasts.msg = "Đã xóa người dùng",
                    this.toasts.type = "success",
                    this.toasts.duration = 2000
                this.toastjs();
            } catch (error) {
                console.log(error);
                this.toasts.title = "Warning",
                    this.toasts.msg = "Tài khoản không phải ADMIN",
                    this.toasts.type = "warn",
                    this.toasts.duration = 2000
                this.toastjs();
            }
        },
        // updateuserindex(index) {
        //     this.$emit("update:activeUser", index)
        // }
    }
}
</script>
<template>
    <div style="padding-left: 100px; padding-top: 10px; width: 1190px;">
        <ul class="list-group">
            <table class="table">
                <thead>
                    <tr class="row">
                        <th class="col-3"  style="padding-left: 60px;" scope="col">Tài khoản</th>
                        <th class="col-2"  style="padding-left: 50px;" scope="col">Số lượng</th>
                        <th class="col-3" style="padding-left: 40px;" scope="col">Địa chỉ</th>
                        <th class="col-2" style="padding-left: 0px;" scope="col">Trạng thái</th>
                        <th class="col-2" style="padding-left: 40px;" scope="col">Xóa</th>

                    </tr>
                </thead>
                <tbody>
                    <td>
                        <li class=" row user-item d-flex justify-content-between" v-for="(order, index) in orders"
                            :key="order._id"
                            style="border: 1px solid #2e1c11; margin: 15px;  border-radius: 10px;">
                            <span class="col-3">{{ order.userId }}</span>
                            <span style="margin-left: 17px;" class="col-1">{{ order.quantity }}</span>
                            <span style="padding-left: 50px;" class="col-3">{{ order.address }}</span>
                            <span style="padding-left: 20px;" class="col-2">{{ order.status }}</span>

                            <i class="col-2 fa-solid fa-trash" style="color: rgb(249, 135, 135); font-size: 20px; padding-left: 70px;"
                                @click="delorder(order._id)">
                            </i>
                        </li>
                    </td>
                </tbody>
            </table>
        </ul>
    </div>
    <toastsVue></toastsVue>

</template>
<style scoped>
.list-group-item:hover {
    background-color: #c62704;
    color: azure;
}
</style>