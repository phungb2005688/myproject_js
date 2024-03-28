<template>
    <HeaderShop></HeaderShop>
    <div class="container" data-aos="fade-up">
        <div class="row">
            <div class="col-lg-12 text-center mb-5 pt-3">
                <h1 class="page-title">VỀ CỬA HÀNG CHÚNG TÔI</h1>
            </div>
        </div>

        <div class="row mb-5">

            <div class="d-md-flex post-entry-2 half">
                <a href="#" class="me-4 thumbnail">
                    <img src="https://www.jonzara.com/Images/Models/Full/17369.Jpg" alt="" class="img-fluid">
                    <!-- <img src="https://bizweb.dktcdn.net/thumb/1024x1024/100/302/551/products/compressed-cropna-2307-4-117-1.jpg?v=1695188390403" alt="" class="img-fluid"> -->

                </a>
                <div class="mt-4 mt-md-0">
                    <div class="post-meta mt-4">Về chúng tôi</div>
                    <h2 class="mb-4 display-4">Lịch sử hình thành</h2>

                    <p>Với niềm đam mê bất tận với những món đồ trang sức nhỏ xinh, năm 2021 Falling & KMD ra đời với mong
                        muốn mang đến cho các cậu những món đồ trang sức bạc nữ tính, hiện đại và tinh tế. Nhiệt huyết, đam
                        mê và sức trẻ là những gì chúng tớ có ở thời điểm ấy. Thật may những sản phẩm của Falling & KMD được
                        các cậu yêu thích và đón nhận. Và cứ thế, cứ thế, chúng tớ phát triển, đến gần hơn với các cô gái.
                    </p>
                    <p>
                        Falling & KMD mong muốn trở thành thương hiệu trang sức bạc hàng đầu dành cho giới trẻ. Tầm nhìn có
                        xa
                        xôi, có khó khăn nhưng chúng tớ tin rằng các cậu vẫn sẽ đồng hành, là nguồn động lực to lớn để chúng
                        tớ cố gắng.
                    </p>
                </div>
            </div>

            <div class="d-md-flex post-entry-2 half mt-5">
                <a href="#" class="me-4 thumbnail order-2">
                    <!-- <img src="https://i.pinimg.com/474x/e5/6d/86/e56d864f8b6279ed6cad83930877fb93.jpg" alt="" class="ps-md-5 img-fluid1"> -->
                    <img src="https://media.jewinston.com/media/catalog/product/cache/1/thumbnail/450x450/9df78eab33525d08d6e5fb8d27136e95/r/i/ri6100034.jpg"
                        alt="" class="ps-md-5 img-fluid1">

                </a>
                <div class="pe-md-5 mt-4 mt-md-0">
                    <div class="post-meta mt-4">SỨ MỆNH &amp; TẦM NHÌN</div>
                    <h2 class="mb-4 display-4">SỨ MỆNH &amp; TẦM NHÌN</h2>

                    <p>Falling & KMD chân thành cảm ơn sự ủng hộ của rất nhiều khách hàng đáng mến trong suốt thời gian qua.
                        Luôn
                        giữ tinh thần phấn đấu không ngừng trong chặng đường hiện thực những giấc mơ của Falling & KMD,
                        chúng
                        mình mong rằng sẽ xây dựng 1 thương hiệu trang sức Việt bền vững và gần gũi với nhiều bạn trẻ khắp
                        nơi. </p>
                    <p>Chúng mình hi vọng tinh thần “Dare to Dream & Trust Yourself - Dám ước mơ & Tin vào chính mình”
                        trong từng món trang sức của Falling & KMD sẽ lan toả đến nhiều cô gái chàng trai hơn nữa.</p>
                </div>
            </div>

        </div>

    </div>
    <div class="container mb-5" data-aos="fade-up">
        <div class="row justify-content-between align-items-lg-center">
            <div class="col-lg-5 mb-4 mb-lg-0">
                <h2 class="display-4 mb-4">Tin mới nhất</h2>
                <p>Chúng tôi có trụ sở tại Cần Thơ và Hồ Chí Minh, chúng tôi sẽ tiếp tục phát triển mỗi năm bằng cách kinh
                    doanh cùng với nhiều nhà sản xuất và nhà phân phối khác nhau của ngành trang sức. Chúng tôi tham dự
                    nhiều triển lãm khác nhau trong khu vực và không ngừng phấn đấu để phát triển thông qua trang web và
                    triển lãm thương mại của mình.</p>
                <p>Không có khách hàng, chúng tôi không có hoạt động kinh doanh. Mong đợi
                    dịch vụ khách hàng tốt nhất của chúng tôi mọi lúc.</p>
            </div>
            <div class="col-lg-6">
                <div class="row">
                    <div class="col-6">
                        <img src="https://esterah.com/wp-content/uploads/2021/04/double-hoop-earrings-450x450.jpg" alt=""
                            class="img-fluid mb-4">
                    </div>
                    <div class="col-6 mt-4">
                        <img src="https://vn-test-11.slatic.net/p/a90a24e192de4c69b7221350bd2875c5.jpg" alt=""
                            class="img-fluid mb-4">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import HeaderShop from '@/components/HeaderShop.vue'
export default {
    components: {
        HeaderShop,
    }
}
</script>
<style>
p {
    color: #2e1c11;
}

.page-title {
    font-size: 25px;
    color: var(--color-black);
}

.img-fluid {
    margin-top: 30px;
    max-width: 70%;
}

.img-fluid1 {
    margin-left: 100px;
    margin-top: 30px;
    max-width: 85%;
}

.post-entry-2 {
    margin-bottom: 30px;
}

.post-entry-2 .post-meta {
    font-size: 11px;
    letter-spacing: 0.07rem;
    text-transform: uppercase;
    font-weight: 600;
    font-family: var(--font-secondary);
    color: rgba(var(--color-black-rgb), 0.4);
    margin-bottom: 10px;
}

.post-entry-2 .thumbnail {
    flex: 0 0 45%;
}

@media (max-width: 960px) {
    .post-entry-2 .thumbnail {
        flex: 0 0 100%;
        margin-bottom: 20px;
    }
}

.post-entry-2.half .thumbnail {
    flex: 0 0 50%;
}

@media (max-width: 768px) {
    .post-entry-2.half .thumbnail {
        flex: 0 0 100%;
        margin-bottom: 20px;
    }
}

.post-entry-2.small-img .thumbnail {
    flex: 0 0 30%;
}

@media (max-width: 768px) {
    .post-entry-2.small-img .thumbnail {
        flex: 0 0 100%;
        margin-bottom: 20px;
    }
}</style>