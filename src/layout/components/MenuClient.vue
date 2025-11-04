<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow-sm py-2">
      <div class="container">
        <router-link to="/" class="navbar-brand d-flex align-items-center gap-2 fs-3 fw-bold">
          <span class="text-warning">🎬</span>
          <span>DZCinema</span>
        </router-link>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
          data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link to="/" class="nav-link" exact-active-class="active"><i class="bi bi-house-door"></i> Trang Chủ</router-link>
            </li>
            <li class="nav-item dropdown">
              <a class="nav-link dropdown-toggle" href="#" id="phimDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                <i class="bi bi-film"></i> Phim
              </a>
              <ul class="dropdown-menu" aria-labelledby="phimDropdown">
                <li><router-link to="/phim/dang-chieu" class="dropdown-item"><i class="bi bi-play-circle me-2"></i>Phim Đang Chiếu</router-link></li>
                <li><router-link to="/phim/sap-chieu" class="dropdown-item"><i class="bi bi-calendar3 me-2"></i>Phim Sắp Chiếu</router-link></li>
              </ul>
            </li>
            <li class="nav-item">
              <router-link to="/bai-viet" class="nav-link"><i class="bi bi-journal-text"></i> Bài Viết</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/about" class="nav-link"><i class="bi bi-info-circle"></i> Về Chúng Tôi</router-link>
            </li>
          </ul>
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
            <li class="nav-item dropdown">
              <a class="nav-link dropdown-toggle d-flex align-items-center" href="#" id="userDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                <img v-if="user" :src="user.avatar" class="rounded-circle me-2 border border-2 border-warning" style="width:36px;height:36px;object-fit:cover;">
                <img v-else src="https://cdn-icons-png.flaticon.com/512/9187/9187604.png" class="rounded-circle me-2 border border-2 border-secondary" style="width:36px;height:36px;object-fit:cover;">
                <span class="d-none d-lg-inline text-white">{{ user ? user.name : 'Tài khoản' }}</span>
              </a>
              <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="userDropdown">
                <template v-if="user">
                  <li><router-link to="/client/profile" class="dropdown-item"><i class="bi bi-person-circle me-2"></i>Thông tin cá nhân</router-link></li>
                  <li><hr class="dropdown-divider"></li>
                  <li><a href="#" class="dropdown-item text-danger" @click.prevent="dangXuat"><i class="bi bi-box-arrow-right me-2"></i>Đăng xuất</a></li>
                </template>
                <template v-else>
                  <li><router-link to="/client/dang-ky" class="dropdown-item"><i class="bi bi-person-plus me-2"></i>Đăng ký</router-link></li>
                  <li><router-link to="/client/dang-nhap" class="dropdown-item"><i class="bi bi-box-arrow-in-right me-2"></i>Đăng nhập</router-link></li>
                </template>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  data() {
    return {
      user: null // Tích hợp lấy user từ localStorage hoặc Vuex nếu đã đăng nhập
    }
  },
  methods: {
    dangXuat() {
      // Logic đăng xuất: có thể clear localStorage, Vuex, rồi reload...
      this.user = null;
      // Ví dụ chuyển hướng
      this.$router.push('/');
    }
  }
}
</script>