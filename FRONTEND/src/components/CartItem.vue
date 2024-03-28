<script>
    export default{
        data(){
            return{
                products:[],
            }
        },
        props:{
            refeshlistcart:Function,
            carts:Array,
        },
        emit:[
            "deleted:cartIndex"
        ],
        methods:{
        deletedcart(index){
            this.$emit("deleted:cartIndex",index);
        },
    },
}
</script>
<template>
    
   <div class="row mb-2 align-items-center" 
            v-for="(item,index) in carts">
          <div class="col-md-2 col-lg-2 col-xl-2">
            <img
                :src="item.img"
                class="img-fluid" alt="Cotton T-shirt">
            </div>
            <div class="col-md-5 col-lg-5 col-xl-5">
                <h6 >{{item.title}}</h6>
                    <div>
                        <span >Màu sắc: <span>{{item.color}}</span></span>
                        <br>
                        <span >Khối lượng: <span>{{item.size}}g</span></span>
                        <br>
                        <span >Số lượng: <span>{{item.quantity}}</span></span>
                      </div>
            </div>
    
            <div class="col-md-4 col-lg-3 col-xl-3 offset-lg-1">
                <h6 style="margin-top: -35px; padding-left: 5px;">Giá</h6>
                <h6 class="mb-0 price" style="padding-left: 5px; padding-top: 15px;">{{(item.price *item.quantity).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")}} đ</h6>
            </div>
            <div class="col-md-1 col-lg-1 col-xl-1 "  @click="deletedcart(index)" style="font-size: 20px; color: rgb(236, 104, 104);">
            <div style="margin-top: -40px; padding-bottom: 5px;">
                <h6 style="font-size: 16px; color: #2e1c11;">Xóa</h6>
            </div>
                <i class="fa-solid fa-trash"></i>
            </div>
            <hr style="width: 1280px; margin-top: 15px; margin-left: 10px; border: 1px solid #3e3e3e;">
    </div>   
     
</template>