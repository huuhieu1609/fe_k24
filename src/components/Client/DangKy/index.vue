<template >
    <div class="col mx-auto">
                         <div class="my-4 text-center">
                             <img src="assets/images/logo-img.png" width="180" alt="" />
                         </div>
                         <div class="card " style="width: 800px;">
                             <div class="card-body">
                                 <div class="border p-4 rounded">
                                     <div class="text-center">
                                         <h3 class="">ĐĂNG KÝ TÀI KHOẢN <H3 class="text-info">DZCINEMA</H3></h3>
                                            <p>Bạn đã có tài khoản? <a href="/admin/dang-nhap">Đăng nhập tại đây</a>
                                         </p>
                                     </div>
                                     
                                     
                                     <div class="form-body">
                                         <form class="row g-3">
                                             <div class="col-6">
                                                 <label class="form-label">Họ và Tên</label>
                                                 <input v-model="dangKy.ho_va_ten" type="text" class="form-control"  placeholder="Nhập họ và tên">
                                             </div>
                                             <div class="col-sm-6">
                                                 <label  class="form-label">Email</label>
                                                 <input v-model="dangKy.email" type="email" class="form-control"  placeholder="Nhập email">
                                             </div>
                                             <div class="col-4">
                                                 <label  class="form-label">Số điện thoại</label>
                                                 <input v-model="dangKy.so_dien_thoai" type="text" class="form-control" placeholder="Nhập số điện thoại">
                                             </div>
                                             <div class="col-4">
                                                 <label  class="form-label">Số cccd</label>
                                                 <input v-model="dangKy.cccd" type="text" class="form-control" placeholder="Nhập số cccd">
                                             </div>
                                             <div class="col-4">
                                                 <label class="form-label">Ngày sinh</label>
                                                 <input v-model="dangKy.ngay_sinh" type="date" class="form-control" placeholder="Nhập ngày sinh">
                                             </div>
                                             <div class="col-6">
                                                 <label  class="form-label">Password</label>
                                                 <div class="input-group" id="show_hide_password">
                                                     <input v-model="dangKy.password" type="password" class="form-control border-end-0"   placeholder="Enter Password"> 
                                                 </div>
                                             </div>
                                             <div class="col-6">
                                                 <label  class="form-label">Re_Password</label>
                                                 <div class="input-group" id="show_hide_password">
                                                     <input v-model="dangKy.re_password" type="password" class="form-control border-end-0"   placeholder="Re Password"> 
                                                 </div>
                                             </div>
                                             
                                             
                                             <div class="col-12">
                                                 <div class="d-grid">
                                                     <button v-on:click="Dang_Ky()" type="button" class="btn btn-success"><i class='bx bx-user'></i>Đăng ký</button>
                                                 </div>
                                             </div>
                                         </form>
                                     </div>
                                 </div>
                             </div>
                         </div>
                     </div>
 </template>
 <script>
 import axios from 'axios';
 
 export default {
     data() {
         return {
         dangKy:{
             ho_va_ten: '',
             email:'',
             so_dien_thoai: '',
             password:'',
             re_password:'',
             cccd:'',
             ngay_sinh:''
         }
         }
     },
     methods:{
         Dang_Ky(){
             axios
             .post("https://be24.deloydz.com/api/39039000-078000-117000-156000/client/dang-ky", this.dangKy)
             .then((res)=>{
                 if(res.data.status == true){
                     alert(res.data.message);
                      localStorage.setItem('ky_dz', res.data.token);
                      this.$router.push("/trang-chu")
                 }else{
                     alert(res.data.message);
                 }
             });
         }
     }
 }
 </script>
 <style >
     
 </style>