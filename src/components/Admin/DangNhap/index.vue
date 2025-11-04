<template>
    <div class="card">
        <div class="card-body">
            <div class="border p-4 rounded">
                <div class="text-center">
                    <h3 class="">ĐĂNG NHẬP HỆ THỐNG</h3>

                </div>
              <div class="form-body">
                    <form class="row g-3">
                        <div class="col-12">
                            <label for="inputEmailAddress" class="form-label">Email Address</label>
                            <input v-model="dangnhap.email" type="email" class="form-control" placeholder="Email Address">
                        </div>
                        <div class="col-12">
                            <label for="inputChoosePassword" class="form-label">Enter Password</label>
                            <div class="input-group" id="show_hide_password">
                                <input v-model="dangnhap.password" type="password" class="form-control border-end-0" placeholder="Enter Password">
                            </div>
                        </div>
                        <div class="col-12">
                            <div class="d-grid">
                                <button v-on:click="dang_nhap()" type="button" class="btn btn-primary"><i class="bx bxs-lock-open"></i>ĐĂNG NHẬP</button>
                            </div>
                        </div>
                    </form>
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
        dangnhap:{
            'email':'',
            'password':''
        }
    }
},
methods:{
    dang_nhap(){
        axios
        .post("https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/dang-nhap", this.dangnhap)
        .then((res)=>{
            if(res.data.status == true){
                alert(res.data.message);
                localStorage.setItem('hieuthuhai', res.data.token);
                this.$router.push('/admin/phim');

            }else{
                alert(res.data.message);
            }
        });
    }
}
}
</script>
<style></style>