<template>
    <div class="main-content">
        <div id="heroMovieCarousel" class="carousel slide hero-carousel" data-bs-ride="carousel">
            <div class="carousel-inner">
                <template v-for="(slide, index) in list_slide" :key="index">
                    <div class="carousel-item" :class="{ 'active': index === 0 }">
                        <img :src="slide.hinh_anh" class="d-block w-100" :alt="slide.ten_phim"
                            style="height: 600px; object-fit: cover; filter: brightness(0.65);">
                        <div class="carousel-caption d-none d-md-block text-start hero-caption">
                            <span class="badge bg-danger mb-3 p-2 text-uppercase fw-bold">🔥 ĐANG CHIẾU ĐỘC QUYỀN</span>
                            <h1 class="fw-bolder display-2 text-shadow">{{ slide.ten_phim }}</h1>
                            <p class="fs-5 mb-4 text-shadow">{{ slide.mo_ta_ngan }}</p>
                            <router-link :to="`/phim/chi-tiet/${slide.id_phim}`"
                                class="btn btn-danger px-5 py-3 mt-2 fw-bold text-uppercase rounded-pill shadow-lg">
                                <i class="fa-solid fa-ticket me-2"></i>Xem Chi Tiết & Đặt Vé
                            </router-link>
                        </div>
                    </div>
                </template>
            </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#heroMovieCarousel"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#heroMovieCarousel"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div>

        <div class="container ">
            <div class="schedule-and-info-section py-5">
                <div class="row mb-5">
                    <div class="col-12">
                        <h2 class="text-2xl font-bold uppercase mb-4 ps-2 border-start border-5 border-danger">Lịch
                            Chiếu Phim
                        </h2>
                    </div>

                    <div class="col-lg-12">
                        <div class="d-flex justify-content-center border-bottom pb-3 mb-4">
                            <button class="btn btn-outline-danger mx-1 fw-bold active" type="button">
                                <span class="d-block">Hôm nay</span>
                                <span class="small">30/10</span>
                            </button>
                            <button class="btn btn-outline-danger mx-1 fw-bold" type="button">
                                <span class="d-block">Thứ Sáu</span>
                                <span class="small">31/10</span>
                            </button>
                            <button class="btn btn-outline-danger mx-1 fw-bold" type="button">
                                <span class="d-block">Thứ Bảy</span>
                                <span class="small">01/11</span>
                            </button>
                            <button class="btn btn-outline-danger mx-1 fw-bold" type="button">
                                <span class="d-block">Chủ Nhật</span>
                                <span class="small">02/11</span>
                            </button>
                            <button class="btn btn-outline-secondary mx-1 fw-bold" type="button">
                                <i class="fa-solid fa-calendar-alt"></i>
                            </button>
                        </div>
                    </div>
                </div>
                <div class="row g-4 movie-list-schedule">
    <template v-for="(movie, index) in list_phim.slice(0, 6)" :key="index">
        <div class="col-lg-2 col-md-3 col-sm-4 col-6 d-flex">
            <div class="card border-0 text-center w-100 h-100 shadow-sm card-schedule-item">
                <router-link :to="`/phim/chi-tiet/${movie.id_phim}`" class="d-block card-img-link">
                    <div class="position-relative overflow-hidden rounded-top" style="height: 250px;">
                        <img :src="movie.hinh_anh" :alt="movie.ten_phim"
                            class="img-fluid object-cover w-100 h-100 rounded-top movie-poster-schedule">

                        <div class="rating-badge position-absolute bottom-0 end-0">
                            <span class="relative z-10 inline-block pr-2">
                                <i class="fa-solid fa-star text-warning small me-1"></i>
                                <span class="text-xl font-semibold text-white align-middle">{{
                                    movie.rating || 'N/A' }}</span>
                            </span>
                        </div>

                        <span class="age__limit position-absolute bottom-0 start-0 m-2">
                            <span class="badge bg-danger text-white px-3 py-1 fw-bold">{{
                                movie.age_limit || 'P' }}</span>
                        </span>
                    </div>
                </router-link>
                
                <div class="card-body p-2 d-flex flex-column">
                    <span class="fw-bold mb-2 text-truncate text-dark">{{ movie.ten_phim }}</span>

                    <div class="mt-auto pt-2 border-top border-light">
                        <button class="btn btn-sm btn-danger me-1 mb-1 px-2 py-1 small fw-bold text-uppercase">
                            14:00
                        </button>
                        <button class="btn btn-sm btn-outline-dark me-1 mb-1 px-2 py-1 small fw-bold text-uppercase">
                            18:30
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </template>
</div>
            </div>
            <div class="row align-items-center mb-5">
                <div class="col-lg-6">
                    <h5 class="text-uppercase text-danger fw-bold mb-2"><i
                            class="fa-solid fa-clapperboard me-2"></i>PHIM NÓNG
                        NHẤT</h5>
                    <h2 class="fw-bold display-5 mb-4">Các Bộ Phim Đang Chiếu Trên Toàn Hệ Thống</h2>
                </div>
                <div class="col-lg-6 text-lg-end">
                    <button class="btn btn-outline-dark px-4 py-2 fw-bold">Xem Toàn Bộ Phim <i
                            class="fa-solid fa-arrow-right-long ms-2"></i></button>
                </div>
            </div>

            <div class="row g-4 movie-grid-section align-items-stretch">
                <div class="col-lg-6 d-flex">
                    <router-link :to="`/phim/chi-tiet/${list_phim[0].id_phim}`"
                        class="card-movie-lg card-effect h-100 w-100">
                        <img :src="list_phim[0].hinh_anh" :alt="list_phim[0].ten_phim"
                            class="img-fluid rounded-4 shadow-lg h-100 w-100 object-cover">
                        <div class="overlay p-4">
                            <span class="badge bg-warning text-dark mb-2 text-uppercase fw-bold">{{
                                list_phim[0].the_loai
                                }}</span>
                            <h3 class="fw-bold text-white display-6">{{ list_phim[0].ten_phim }}</h3>
                            <p class="text-white-50 text-truncate-3">{{ list_phim[0].mo_ta }}</p>
                            <button class="btn btn-sm btn-danger px-4 py-2 rounded-pill fw-bold text-uppercase">
                                <i class="fa-solid fa-cart-shopping me-1"></i> Đặt Vé
                            </button>
                        </div>
                    </router-link>
                </div>
                <div class="col-lg-6 d-flex flex-column justify-content-between">
                    <div class="row g-4 h-100">
                        <template v-for="(value, idx) in list_phim.slice(1, 5)" :key="idx">
                            <div class="col-md-6 d-flex">
                                <router-link :to="`/phim/chi-tiet/${value.id_phim}`"
                                    class="card-movie-sm card-effect flex-grow-1 w-100">
                                    <div
                                        class="card h-100 border-0 shadow-sm rounded-4 overflow-hidden card-hover-zoom d-flex flex-column">
                                        <div class="card-header-image position-relative">
                                            <img :src="value.hinh_anh" :alt="value.ten_phim"
                                                class="card-img-top object-cover movie-poster-sm">
                                            <span
                                                class="badge bg-danger position-absolute top-0 start-0 m-2 px-3 py-2 fw-bold rounded-pill">
                                                MỚI
                                            </span>
                                        </div>
                                        <div class="card-body p-3 d-flex flex-column flex-grow-1">
                                            <h5 class="fw-bold mb-1 text-truncate-custom">{{ value.ten_phim }}</h5>
                                            <small class="text-muted mb-2"><i class="fa-solid fa-user-tie me-1"></i> {{
                                                value.dao_dien }}</small>
                                            <span class="badge bg-secondary mb-1 align-self-start">{{ value.the_loai
                                                }}</span>
                                            <div class="mt-auto">
                                                <button class="btn btn-sm btn-dark w-100 fw-bold">
                                                    <i class="fa-solid fa-info-circle me-1"></i> Chi Tiết
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </router-link>
                            </div>
                        </template>
                    </div>
                </div>
            </div>
        </div>

        <div class="container py-5">
            <div class="row text-center mb-5">
                <div class="col-lg-8 mx-auto">
                    <h5 class="text-uppercase text-info fw-bold mb-2"><i class="fa-solid fa-calendar-alt me-2"></i>SẮP
                        RA MẮT
                    </h5>
                    <h2 class="fw-bold display-5">Phim Sắp Chiếu - Đặt Vé Trước Để Nhận Ưu Đãi!</h2>
                </div>
            </div>

            <div class="row g-4">
                <template v-for="(value, index) in list.slice(0, 3)" :key="index">
                    <div class="col-lg-4 col-md-6 d-flex">
                        <div class="card h-100 border-0 shadow-lg rounded-4 overflow-hidden">
                            <div class="position-relative">
                                <img :src="value.hinh_anh" :alt="value.ten_phim" class="card-img-top object-cover"
                                    style="height: 350px;">
                                <div
                                    class="position-absolute bottom-0 start-0 bg-dark bg-opacity-75 text-white p-2 w-100">
                                    <h4 class="mb-0 fw-bold">{{ value.ten_phim }}</h4>
                                    <small class="text-info">{{ value.the_loai }} | {{ value.thoi_luong }} phút</small>
                                </div>
                            </div>
                            <div class="card-body d-flex flex-column p-4">
                                <p class="text-muted small flex-grow-1">Đạo diễn: <b>{{ value.dao_dien }}</b></p>
                                <div class="d-flex justify-content-between align-items-center mb-3">
                                    <span class="fw-bold text-danger"><i class="fa-solid fa-clock me-1"></i> Khởi chiếu:
                                        {{ value.ngay_khoi_chieu }}</span>
                                    <span class="badge bg-info p-2">SẮP CHIẾU</span>
                                </div>
                                <button class="btn btn-info w-100 fw-bold py-2 text-uppercase">
                                    <i class="fa-solid fa-bell me-2"></i>Đặt Thông Báo
                                </button>
                            </div>
                        </div>
                    </div>
                </template>
            </div>

        </div>
        <div class="row g-4">
            <div class="col-lg-12">
                <div class="cinema__info mt-3">
                    <iframe
                        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3834.020501865913!2d108.18898127503956!3d16.06497128461756!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x314219b932c0217b%3A0x6e26b1c3e38c92a9!2zR2FsYXh5IENpbmVtYSDEkMOgIE7hurNuZw!5e0!3m2!1sen!2s-!4v1633512000000!5m2!1sen!2s-&hl=vi"
                        class="w-100" style="height: 400px; border:0;" allowfullscreen="" loading="lazy"
                        referrerpolicy="no-referrer-when-downgrade">
                    </iframe>
                </div>
            </div>
        </div>


    </div>
</template>

<script>
// Không cần import axios nếu bạn chỉ sử dụng dữ liệu tĩnh
export default {
    data() {
        return {
            // list: Dữ liệu cho PHIM SẮP CHIẾU
            list: [
                {
                    id_phim: 5,
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.XIhbaa1HLt-hyXaPZ34qgQHaEH?pid=Api&P=0&h=220',
                    ten_phim: 'NGƯỜI HÙNG VÔ DANH',
                    dao_dien: 'Zack Snyder',
                    the_loai: 'Siêu Anh Hùng',
                    ngay_khoi_chieu: '25/12/2025',
                    thoi_luong: 125
                },
                {
                    id_phim: 6,
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.uCwhEVo46ZNgmGtUAYvVyQHaD3?pid=Api&P=0&h=220',
                    ten_phim: 'TRUYỀN THUYẾT BIỂN SÂU',
                    dao_dien: 'James Cameron',
                    the_loai: 'Giả Tưởng',
                    ngay_khoi_chieu: '01/01/2026',
                    thoi_luong: 140
                },
                {
                    id_phim: 7,
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.BK_WWkA-Fuxu5rQQFje-CQHaEa?pid=Api&P=0&h=220',
                    ten_phim: 'CUỘC ĐỜI CỦA EM',
                    dao_dien: 'Quentin Tarantino',
                    the_loai: 'Tâm Lý',
                    ngay_khoi_chieu: '10/02/2026',
                    thoi_luong: 110
                },
                {
                    id_phim: 7,
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.BK_WWkA-Fuxu5rQQFje-CQHaEa?pid=Api&P=0&h=220',
                    ten_phim: 'CUỘC ĐỜI CỦA EM',
                    dao_dien: 'Quentin Tarantino',
                    the_loai: 'Tâm Lý',
                    ngay_khoi_chieu: '10/02/2026',
                    thoi_luong: 110
                },
                {
                    id_phim: 7,
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.BK_WWkA-Fuxu5rQQFje-CQHaEa?pid=Api&P=0&h=220',
                    ten_phim: 'CUỘC ĐỜI CỦA EM',
                    dao_dien: 'Quentin Tarantino',
                    the_loai: 'Tâm Lý',
                    ngay_khoi_chieu: '10/02/2026',
                    thoi_luong: 110
                },
            ],

            // list_phim: Dữ liệu cho PHIM ĐANG CHIẾU (Đã đồng bộ với Template)
            // Thay thế list_phim hiện tại của bạn bằng đoạn mã dưới đây:
list_phim: [
    {
        id_phim: 1,
        // Cục Vàng Của Ngoại
        hinh_anh: 'https://tse3.mm.bing.net/th/id/OIP.ostytIIGT01OkwPCBRSLxAHaKe?pid=Api&P=0&h=220',
        ten_phim: 'CỤC VÀNG CỦA NGOẠI',
        dao_dien: 'Tâm lý, Gia đình',
        the_loai: 'Tâm lý, Gia đình',
        mo_ta: 'Tác phẩm ấm áp về tình cảm bà cháu, đang nhận được nhiều phản hồi tích cực từ khán giả Việt.',
        rating: 9.1, 
        age_limit: 'T13'
    },
    {
        id_phim: 2,
        // Tử Chiến Trên Không
        hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.MMpsyG6ALaDMqvsb2g_7DwHaJT?pid=Api&P=0&h=220',
        ten_phim: 'TỬ CHIẾN TRÊN KHÔNG (Bom Tấn)',
        dao_dien: 'Hành động, Hồi hộp',
        the_loai: 'Hành động, Hồi hộp',
        mo_ta: 'Siêu phẩm hành động với những cảnh quay trên không đỉnh cao, giữ vững phong độ suất chiếu sau nhiều tuần.',
        rating: 8.8,
        age_limit: 'T16'
    },
    {
        id_phim: 3,
        // Nhà Ma Xó
        hinh_anh: 'https://tse1.mm.bing.net/th/id/OIP.Zw6Tjw2kDrxyYUSmAdhe5QHaJQ?pid=Api&P=0&h=220',
        ten_phim: 'NHÀ MA XÓ (Mới ra mắt)',
        dao_dien: 'Kinh dị Việt Nam',
        the_loai: 'Kinh Dị, Tâm Linh',
        mo_ta: 'Phim kinh dị Việt mới nhất, khai thác các câu chuyện dân gian rùng rợn và được khán giả chờ đợi trong mùa Halloween.',
        rating: 7.5,
        age_limit: 'T16'
    },
    {
        id_phim: 4,
        // Mục Sư, Thầy Đồng và Quỷ Âm Trì
        hinh_anh: 'https://tse1.mm.bing.net/th?id=OIF.2ZPT5s%2b0dm39z365zn56pQ&pid=Api&P=0&h=220',
        ten_phim: 'MỤC SƯ VÀ QUỶ ÂM TRÌ',
        dao_dien: 'Kinh dị, Bí ẩn',
        the_loai: 'Kinh Dị/Bí ẩn',
        mo_ta: 'Phim kinh dị nước ngoài với đề tài trừ tà, dự kiến gây sốt phòng vé vào cuối tuần Halloween.',
        rating: 7.9,
        age_limit: 'T18'
    },
    {
        id_phim: 5,
        // Phá Đám: Sinh Nhật Mẹ
        hinh_anh: 'https://tse3.mm.bing.net/th/id/OIP.PCAZhISe-hQKlgd1Nc1YHQHaJQ?pid=Api&P=0&h=220',
        ten_phim: 'PHÁ ĐÁM: SINH NHẬT MẸ',
        dao_dien: 'Hài, Gia đình',
        the_loai: 'Hài Hước, Gia Đình',
        mo_ta: 'Một bộ phim giải trí nhẹ nhàng, hài hước, thích hợp cho các buổi xem phim thư giãn cùng gia đình và bạn bè.',
        rating: 8.0,
        age_limit: 'T13'
    },
    // Thêm một phim hoạt hình đang hot cho đa dạng
    {
        id_phim: 6,
        // Phim Shin Cậu Bé Bút Chì
        hinh_anh: 'https://tse1.mm.bing.net/th/id/OIP.uCluLLtgLEsdajKKnYhfHQHaLH?pid=Api&P=0&h=220',
        ten_phim: 'PHIM SHIN CẬU BÉ BÚT CHÌ',
        dao_dien: 'Hoạt hình, Hài hước',
        the_loai: 'Hoạt Hình',
        mo_ta: 'Phần mới của series hoạt hình quốc dân, luôn thu hút lượng lớn khán giả nhỏ tuổi và gia đình.',
        rating: 9.3,
        age_limit: 'P'
    },
],

            // list_slide: Dữ liệu cho BANNER
            list_slide: [
                {
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.nxRe2MwVwvXZvPkH36q-7QHaEo?pid=Api&P=0&h=220',
                    ten_phim: 'VŨ TRỤ KỲ VĨ: HÀNH TINH MỚI',
                    mo_ta_ngan: 'Hành trình khám phá dải ngân hà với những bí ẩn chưa từng được tiết lộ. Tác phẩm bom tấn không thể bỏ qua!',
                    id_phim: 8
                },
                {
                    hinh_anh: 'https://tse2.mm.bing.net/th/id/OIP.0rhUdKP9h3fAKm49YjYVcgHaEc?pid=Api&P=0&h=220',
                    ten_phim: 'ÁNH SÁNG CUỐI CON ĐƯỜNG',
                    mo_ta_ngan: 'Một bộ phim tâm lý xã hội sâu sắc, với diễn xuất đỉnh cao và kịch bản bất ngờ. Đang có suất chiếu đặc biệt.',
                    id_phim: 9
                },
            ]
        }
    },
    // Nếu sử dụng dữ liệu tĩnh trong data(), bạn không cần hàm loadData() hoặc mounted()
    // Nếu sau này bạn muốn tích hợp API, bạn sẽ cần thêm lại mounted() và loadData()
}
</script>

<style scoped>
/* GENERAL STYLES */
.hero-carousel {
    margin-bottom: 50px;
}

.hero-caption {
    bottom: 20% !important;
    left: 8% !important;
    max-width: 600px;
}

.text-shadow {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

.object-cover {
    object-fit: cover;
}

.rounded-pill {
    border-radius: 50rem !important;
}

/* 2. Now Showing Section (Asymmetrical Cards) */
.card-movie-lg {
    display: block;
    position: relative;
    height: 500px;
    /* Chiều cao cố định cho card lớn */
    overflow: hidden;
    border-radius: 1rem;
    transition: transform 0.3s ease;
}

.card-movie-lg:hover {
    transform: translateY(-5px);
}

.card-movie-lg img {
    filter: brightness(0.85);
    transition: filter 0.3s ease;
}

.card-movie-lg:hover img {
    filter: brightness(0.7);
}

.card-movie-lg .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(transparent, rgba(0, 0, 0, 0.8));
}

.card-movie-lg .overlay h3 {
    font-size: 2.5rem;
}

.card-movie-sm {
    display: block;
    height: 100%;
}

.card-movie-sm:hover .card {
    box-shadow: 0 0.5rem 1rem rgba(220, 53, 69, 0.2) !important;
    /* Đổ bóng màu đỏ khi hover */
    transform: translateY(-3px);
    transition: all 0.3s ease;
}

/* 3. Upcoming Movies (Vertical Cards) */
.card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
}

/* Custom Colors */
.text-danger {
    color: #dc3545 !important;
}

.bg-danger {
    background-color: #dc3545 !important;
    border-color: #dc3545 !important;
}

.btn-danger {
    background-color: #dc3545 !important;
    border-color: #dc3545 !important;
}

.text-info {
    color: #0d6efd !important;
}

.bg-info {
    background-color: #0d6efd !important;
}

.btn-info {
    background-color: #0d6efd !important;
    border-color: #0d6efd !important;
    color: white !important;
}
</style>