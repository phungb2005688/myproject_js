<script>
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import HeaderShop from "../components/HeaderShop.vue";
import EditUser from "../components/EditUser.vue";
import toastsVue from "../components/toasts.vue";
export default {
	data(){
		return{
			checkedit:false,
		}
	},
	components:{
		HeaderShop,
		EditUser,
		toastsVue
	},
	computed: {
		...mapState(useAuthStore, {
			currentUser: "user",
		}),
	},
	methods:{
		showedit(){
			if(!this.checkedit){
				this.checkedit=true;
			}
			else{
				this.checkedit=false;
			}
		},

	}
};
</script>
<template>
	<HeaderShop></HeaderShop>
	<toastsVue></toastsVue>
	<div style="display: flex; min-height: 400px; padding-top: 50px;">
	<div v-if="currentUser" class="imageChim">
		<header>
			<h3 style="text-align: center; font-weight: 600; padding-top: 15px;">
				THÔNG TIN KHÁCH HÀNG 
			</h3>
		</header>
		<div class="row">
			<div class="col-md-8 mt-2">
				<p class="text-break">
					<strong>Tên tài khoản:</strong>
					{{ currentUser.username }}
				</p>
				<p class="text-break">
					<strong>Email:</strong>
					{{ currentUser.email }}
				</p>
			</div>
		</div>
		<router-link to="/">
			<!-- <button class="btn btn-danger">Trở về</button> -->
		</router-link>
		<button class="btn edit-button" style="margin-left: 200px;" @click="showedit">Chỉnh sửa</button>
	</div>
	<div v-if="checkedit" style="display: flex;flex-direction: column;">
			<EditUser :user="currentUser"></EditUser>
	</div>	
</div>
</template>
<style>
.imageChim{
	background-image: url(https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQDwkMYGdjGfSo_12Ko97WM8tgByu_3UgnuA9LJsgWBYYEGEdzW1qSa-fl9Qe376i44tVY&usqp=CAU);
	border-radius: 20px;
	height: 240px;
	margin-left: 100px; 
	width: 500px;
}
.text-break{
	min-width: 300px;
	border: 1px solid #ccc;
	margin-left: 100px;
	border-radius: 10px;
	padding: 10px;
	background-color: #fff;
}
.edit-button{
	background-color: #8d8d8d;
	color: white;
}
.edit-button:hover{
	background-color: #2e1c11;
	color: white;
	font-weight: 600;
}
</style>

