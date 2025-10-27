<template>
    <div class="row">
        <div class="col-lg-12">
            <div class="card radius-10 border-top border-0 border-3 border-info">
                <div class="card-header d-flex justify-content-between">
                    <h4 class="mt-2"><b>DANH SÁCH VÉ</b></h4>
                    <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addModal">
                        Thêm Suất Chiếu
                    </button>
                </div>
                <div class="card-body table-responsive">
                    <div class="input-group mb-3">
                        <input type="text" class="form-control" placeholder="Tìm kiếm khách hàng...">
                        <button class="btn btn-success input-group-text" style="width: 155px;">Tìm
                            kiếm</button>
                    </div>
                    <div class="table-responsive">
                        <table class="table table-bordered table-hover">
                            <thead>
                                <tr class="bg-primary text-light text-nowrap">
                                    <th class="text-center">#</th>
                                    <th class="text-center">Mã Vé</th>
                                    <th class="text-center">Khách Hàng</th>
                                    <th class="text-center">Tên Phim</th>
                                    <th class="text-center">Suất Chiếu</th>
                                    <th class="text-center">Ghế</th>
                                    <th class="text-center">Giá Vé</th>
                                    <th class="text-center">Trạng Thái</th>
                                    <th class="text-center">Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr class="text-nowrap" v-for="(item, index) in list_ve" :key="index">
                                    <th class="align-middle text-center">{{ index + 1 }}</th>
                                    <td class="align-middle">{{ item.ma_ve }}</td>
                                    <td class="align-middle text-center">
                                        <template v-for="(item_1, index_1) in list_khach_hang" :key="index_1">
                                            <span v-if="item_1.id == item.id_don_hang">{{ item_1.ho_va_ten }}</span>
                                        </template>
                                    </td>
                                    <td class="align-middle text-center">
                                        <template v-for="(item_1, index_1) in list_suat_chieu" :key="index_1">
                                            <span v-if="item_1.id == item.id_suat_chieu">{{ item_1.ten_phim }}</span>
                                        </template>
                                    </td>
                                    <td class="align-middle text-center">
                                        <template v-for="(item_1, index_1) in list_suat_chieu" :key="index_1">
                                            <span v-if="item_1.id == item.id_suat_chieu">{{ item_1.ngay_chieu }} - {{ item_1.thoi_gian_bat_dau }}</span>
                                        </template>
                                    </td>
                                    <td class="align-middle text-center">{{ item.ten_ghe }}</td>
                                    <td class="align-middle text-center">{{ formatMoney(item.gia_ve) }}</td>
                                    <td class="align-middle text-center">
                                        <button v-if="item.tinh_trang == 1" class="btn btn-success w-100">
                                            Đã Thanh Toán
                                        </button>
                                        <button v-else-if="item.tinh_trang == 0" class="btn btn-warning text-light w-100">
                                            Chưa Thanh Toán
                                        </button>
                                        <button v-else class="btn btn-danger w-100">
                                            Đã Hủy
                                        </button>
                                    </td>
                                    <td class="align-middle text-center" style="width: 200px;">
                                        <button class="btn btn-info text-light me-2" data-bs-toggle="modal"
                                            data-bs-target="#updateModal"
                                            v-on:click="Object.assign(update_ve, item)">
                                            Cập nhật
                                        </button>
                                        <button class="btn btn-danger" data-bs-toggle="modal"
                                            data-bs-target="#deleteModal"
                                            v-on:click="Object.assign(delete_ve, item)">
                                            Xóa
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Thêm Mới -->
    <div class="modal fade" id="addModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Thêm Vé Mới</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Khách Hàng</label>
                            <select v-model="create_ve.id_don_hang" class="form-select">
                                <option value="0">Chọn khách hàng</option>
                                <option v-for="(item, index) in list_khach_hang" :key="index" :value="item.id">
                                    {{ item.ho_va_ten }}
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Suất Chiếu</label>
                            <select v-model="create_ve.id_suat_chieu" class="form-select">
                                <option value="0">Chọn suất chiếu</option>
                                <option v-for="(item, index) in list_suat_chieu" :key="index" :value="item.id">
                                    {{ item.ten_phim }}
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Ghế</label>
                            <select v-model="create_ve.id_phong_chieu" class="form-select">
                                <option value="0">Chọn ghế</option>
                                <option v-for="(item, index) in list_ghe" :key="index" :value="item.id">
                                    {{ item.ten_ghe }}
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Trạng Thái</label>
                            <select v-model="create_ve.tinh_trang" class="form-select">
                                <option value="1">Đã Thanh Toán</option>
                                <option value="0">Chưa Thanh Toán</option>
                                <option value="2">Đã Hủy</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button @click="addVe()" type="button" class="btn btn-primary" data-bs-dismiss="modal">
                        Thêm mới
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Cập Nhật -->
    <div class="modal fade" id="updateModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-xl">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Cập Nhật Thông Tin Suất Chiếu</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Khách Hàng</label>
                            <select v-model="update_ve.id_don_hang" class="form-select">
                                <option value="0">Chọn khách hàng</option>
                                <option v-for="(item, index) in list_khach_hang" :key="index" :value="item.id">
                                    {{ item.ho_va_ten }}
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Suất Chiếu</label>
                            <select v-model="update_ve.id_suat_chieu" class="form-select">
                                <option value="0">Chọn suất chiếu</option>
                                <option v-for="(item, index) in list_suat_chieu" :key="index" :value="item.id">
                                    {{ item.ten_phim }}
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Ghế</label>
                            <select v-model="update_ve.id_phong_chieu" class="form-select">
                                <option value="0">Chọn ghế</option>
                                <option v-for="(item, index) in list_ghe" :key="index" :value="item.id">
                                    {{ item.ten_ghe }} 
                                </option>
                            </select>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label  class="form-label">Trạng Thái</label>
                            <select v-model="update_ve.tinh_trang"  class="form-select">
                                <option value="1">Đã Thanh Toán</option>
                                <option value="0">Chưa Thanh Toán</option>
                                <option value="2">Đã Hủy</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button @click="updateVe()" type="button" class="btn btn-success" data-bs-dismiss="modal">
                        Cập nhật
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Xóa -->
    <div class="modal fade" id="deleteModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Xóa Suất Chiếu</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="alert alert-danger" role="alert">
                        Bạn có chắc chắn muốn xóa suất chiếu phim
                        <strong>{{ delete_suat_chieu.ten_phim }}</strong> vào ngày <strong>{{ delete_suat_chieu.ngay_chieu }}</strong>?
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button @click="deleteVe()" type="button" class="btn btn-danger" data-bs-dismiss="modal">
                        Xác nhận
                    </button>
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
            list_khach_hang: [],
            list_suat_chieu: [],
            list_ghe: [],
            create_ve: {
                id_don_hang: '',
                id_suat_chieu: '',
                id_phong_chieu: '',
                tinh_trang: '',
            },
            update_ve: {
                id: '',
                id_don_hang: '',
                id_suat_chieu: '',
                id_phong_chieu: '',
                tinh_trang: '',
            },
            delete_ve: {
                id: '',
                ma_ve: '',
                gia_ve: '',
                id_don_hang: '',
                id_suat_chieu: '',
                ten_ghe: '',
                tinh_trang: '',
            },
        }
    },
    methods: {
        loadDataVe() {
            axios
                .get('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/ve/get-data')
                .then((res) => {
                    this.list_ve = res.data.data;
                });
        },
        loadDataKhachHang() {
            axios
                .get('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/khach-hang/get-data')
                .then((res) => {
                    this.list_khach_hang = res.data.data;   
                });
        },
        loadDataSuatChieu() {
            axios
                .get('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/suat-chieu/get-data')
                .then((res) => {
                    this.list_suat_chieu = res.data.data;
                });
        },
        loadDataGhe() {
            axios
                .get('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/ghe/get-data')
                .then((res) => {
                    this.list_ghe = res.data.data;
                });
        },
        addVe() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/ve/add-data', this.create_ve)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataVe();
                        alert(res.data.message);
                    }
                });
        },
        updateVe() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/ve/update', this.update_ve)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataVe();
                        alert(res.data.message);
                    }
                });
        },
        deleteVe() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/ve/delete', this.delete_ve)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataVe();
                        alert(res.data.message);
                    }
                });
        },
        formatMoney(number) {
            return new Intl.NumberFormat("vi-VI", { style: "currency", currency: "VND" }).format(number).replace('₫','VND');
        }
    },
    mounted() {
        this.loadDataVe();
        this.loadDataKhachHang();
        this.loadDataSuatChieu();
        this.loadDataGhe();
    },
}
</script>
<style></style>