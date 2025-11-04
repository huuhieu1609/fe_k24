<template >
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/7.0.1/css/all.min.css"
      integrity="sha512-2SwdPD6INVrV/lHTZbO2nodKhrnDdJK9/kg2XD1r9uGqPo1cUbujc+IYdlYdEErWNu69gVcYgdxlmVmzTWnetw=="
      crossorigin="anonymous" referrerpolicy="no-referrer" />
  <div id="carouselExampleIndicators" class="carousel slide">
      <div class="carousel-indicators">
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"
              aria-current="true" aria-label="Slide 1"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"
              aria-label="Slide 2"></button>
          <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"
              aria-label="Slide 3"></button>
      </div>
      <div class="carousel-inner">
          <template v-for="(value, index) in dataslide" :key="index">
              <div class="carousel-item " :class="index === 0 ? 'active' : ''">

                  <img style="height: 600px; " v-bind:src="value.hinh_anh" class="d-block w-100" alt="...">


              </div>
          </template>
      </div>
      <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleIndicators"
          data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
      </button>
      <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleIndicators"
          data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
      </button>
  </div   >
  <div class="container">
      <div class="row">
      <h2 class="text-center mt-3">Phim Sắp Chiếu</h2>
     <template v-for="(value,index) in PhimSapChieu" :key="index">
      <div class="col-lg-3 ">
          
          <img style="height: 400px; width: 100%;" :src="value.hinh_anh" alt="">
          <p class="mt-2"><b>{{ value.ten_phim }}</b></p>
          
     
     </div>
     </template>
  </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
   data() {
      return {
          dataslide: [],
          PhimSapChieu:[],
          
      }
  },
  mounted() {
      this.getData();
      this.getPhimSapChieu();
     
  },
  

  methods: {
      getData() {
          axios
              .get("https://be24.deloydz.com/api/34034000-068000-102000-136000/client/trang-chu/get-data")
              .then((res) => {
                  this.dataslide = res.data.data_slide;
              });
      },
      getPhimSapChieu() {
          axios
              .get("https://be24.deloydz.com/api/34034000-068000-102000-136000/client/phim-sap-chieu/get-data")
              .then((res) => {
                  this.PhimSapChieu=res.data.data;
              });
      },
      
  },
}

</script>
<style >
  
</style>