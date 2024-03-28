<script>
import UserService from "../services/User.service";
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
        users: Array,
        refeshlist: Function,
        activeUser: { type: Number, default: -1 },
    },
    emits: ['update:activeUser'],
    methods: {
        toastjs,
        async deluser(id) {
            try {
                await UserService.delete(id);
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
        updateuserindex(index) {
            this.$emit("update:activeUser", index)
        }
    }
}
</script>
<template>
    <div style="padding-left: 100px; padding-top: 10px; width: 750px;">
        <ul class="list-group">
            <table class="table">
                <thead>
                    <tr class="row">
                        <th class="col-4"  style="padding-left: 40px;" scope="col">Tên tài khoản</th>
                        <th class="col-5"  style="padding-left: 50px;" scope="col">Email</th>
                        <th class="col-3" style="padding-left: 40px;" scope="col">Xóa</th>
                    </tr>
                </thead>
                <tbody>
                    <td>
                        <li class=" row user-item d-flex justify-content-between" v-for="(user, index) in users"
                            v-show="!user.isAdmin" :key="user._id" @click="updateuserindex(index)"
                            style="border: 1px solid #2e1c11; margin: 15px;  border-radius: 10px;">
                            <span class="col-4">{{ user.username }}</span>
                            <span class="col-6">{{ user.email }}</span>
                            <i class="col-2 fa-solid fa-trash" style="color: rgb(249, 135, 135); font-size: 20px;"
                                @click="deluser(user._id)">
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