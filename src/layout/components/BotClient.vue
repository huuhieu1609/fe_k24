<template>
     <div class="bg-dark text-white py-5">
            <div class="container">
                <div class="row align-items-center">
                    <div class="col-lg-6 p-4">
                        <h2 class="fw-bold display-5 text-warning mb-4">Đừng Bỏ Lỡ Suất Chiếu Yêu Thích Của Bạn!</h2>
                        <p class="fs-5 mb-4">Đặt vé ngay hôm nay để có chỗ ngồi tốt nhất và trải nghiệm những thước phim tuyệt vời trên màn hình lớn.</p>
                        <router-link to="/dat-ve" class="btn btn-danger px-5 py-3 fw-bold text-uppercase rounded-pill shadow-lg me-3">
                            <i class="fa-solid fa-calendar-check me-2"></i>ĐẶT VÉ TRỰC TUYẾN
                        </router-link>
                        <router-link to="/lien-he" class="btn btn-outline-light px-5 py-3 fw-bold text-uppercase rounded-pill">
                            Liên Hệ
                        </router-link>
                    </div>
                    <div class="col-lg-6 p-4">
                        <h4 class="fw-bold mb-3 text-info"><i class="fa-solid fa-clock me-3"></i>GIỜ HOẠT ĐỘNG HÀNG NGÀY</h4>
                        <ul class="list-unstyled">
                            <li class="d-flex justify-content-between py-2 border-bottom">
                                <span class="fw-semibold">Thứ 2 - Thứ 5:</span>
                                <span class="text-warning fw-bold">9:00 - 23:00</span>
                            </li>
                            <li class="d-flex justify-content-between py-2 border-bottom">
                                <span class="fw-semibold">Thứ 6 - Chủ Nhật:</span>
                                <span class="text-warning fw-bold">8:00 - 00:00</span>
                            </li>
                            <li class="d-flex justify-content-between py-2">
                                <span class="fw-semibold">HOTLINE HỖ TRỢ:</span>
                                <span class="text-danger fw-bold fs-4">1900 6000</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
export default {};
</script>