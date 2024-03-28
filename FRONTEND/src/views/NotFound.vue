<template>
    <div class="page mt-4 mb-5" >
            <div class="pt-4 imagefound">
                <div class="notfound">
                    <h6>Oops, không thể tìm thấy trang.</h6> Quay lại
                    <router-link to="/" style="color: brown; font-weight: 700;">Trang chủ.</router-link>
                </div>

            </div>
    </div>
</template>
<style>
.imagefound {
    background-image: url(https://st2.depositphotos.com/7023650/47826/v/450/depositphotos_478264426-stock-illustration-404-error-page-not-found.jpg);
    height: 310px;
    width: 600px;
    margin-left: 350px;
}
.notfound{
    width: 300px;
    margin-top: 200px;
    margin-left: 270px;
    border: 3px dashed;
    border-radius: 10px;
    padding: 10px;
}
</style>