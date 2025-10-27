<template>
    <div class="row">
        <div class="col-lg-12">
            <div class="card radius-10 border-top border-0 border-3 border-info">
                <div class="card-header d-flex justify-content-between">
                    <h4 class="mt-2"><b>DANH SÁCH BÀI VIẾT</b></h4>
                    <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addModal">
                        Thêm Bài Viết
                    </button>
                </div>
                <div class="card-body table-responsive">
                    <div class="table-responsive">
                        <table class="table table-bordered table-hover">
                            <thead>
                                <tr class="bg-primary text-light ">
                                    <th class="text-center">#</th>
                                    <th class="text-center">Tiêu Đề</th>
                                    <th class="text-center">Mô Tả Ngắn</th>
                                    <th class="text-center">Nội Dung</th>
                                    <th class="text-center">Hình Ảnh</th>
                                    <th class="text-center">Tag</th>
                                    <th class="text-center">Trạng Thái</th>
                                    <th class="text-center">Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(item, index) in list_bai_viet" :key="index">
                                    <th class="align-middle text-center">{{ index + 1 }}</th>
                                    <td class="align-middle">{{ item.tieu_de }}</td>
                                    <td class="align-middle">{{ item.mo_ta_ngan }}</td>
                                    <td class="align-middle text-center">
                                        <i class="fa-solid fa-circle-info text-primary fa-2x"></i>
                                    </td>
                                    <td class="align-middle text-center">
                                        <img v-bind:src="item.hinh_anh" alt="" class="img-fluid rounded-3"
                                            style="height: 100px; width: 150px;">
                                    </td>
                                    <td class="align-middle">
                                        <span v-for="(tag, i) in tagArr(item.tag)" :key="i" class="badge bg-primary me-1">
                                            {{ tag }}
                                        </span>
                                    </td>
                                    <td class="align-middle text-center">
                                        <button v-if="item.tinh_trang == 1" class="btn btn-success w-100">
                                            Hoạt Động
                                        </button>
                                        <button v-else class="btn btn-danger w-100">
                                            Tạm Tắt
                                        </button>
                                    </td>
                                    <td class="align-middle text-center" style="width: 200px;">
                                        <button class="btn btn-info text-light me-2" data-bs-toggle="modal"
                                            data-bs-target="#updateModal"
                                            v-on:click="Object.assign(update_bai_viet, item)">
                                            Cập nhật
                                        </button>
                                        <button class="btn btn-danger" data-bs-toggle="modal"
                                            data-bs-target="#deleteModal"
                                            v-on:click="Object.assign(delete_bai_viet, item)">
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
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Thêm Bài Viết Mới</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Tiêu Đề</label>
                            <input v-model="create_bai_viet.tieu_de" type="text" class="form-control" placeholder="Nhập tiêu đề cho bài viết về phim..." />
                        </div>
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Mô Tả Ngắn</label>
                            <textarea v-model="create_bai_viet.mo_ta_ngan" class="form-control" placeholder="Mô tả ngắn về nội dung bài viết" rows="2"></textarea>
                        </div>
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Nội Dung</label>
                            <textarea v-model="create_bai_viet.noi_dung" class="form-control" placeholder="Nội dung chi tiết của bài viết về phim, review, tin tức điện ảnh,..." rows="4"></textarea>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Hình Ảnh</label>
                            <input v-model="create_bai_viet.hinh_anh" type="text" class="form-control" placeholder="URL hình ảnh minh họa" />
                        </div>
                        <div class="col-md-3 mb-3">
                            <label class="form-label">Tag</label>
                            <input v-model="create_bai_viet.tag" type="text" class="form-control" placeholder="Tag A, Tag B, Tag C"/>
                        </div>
                        <div class="col-md-3 mb-3">
                            <label class="form-label">Trạng Thái</label>
                            <select v-model="create_bai_viet.tinh_trang" class="form-select">
                                <option value="1">Hiển Thị</option>
                                <option value="0">Tạm Tắt</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="addBaiViet()">
                        Thêm mới
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Cập Nhật -->
    <div class="modal fade" id="updateModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Cập Nhật Thông Tin Khách Hàng</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Tiêu Đề</label>
                            <input v-model="update_bai_viet.tieu_de" type="text" class="form-control" placeholder="Nhập tiêu đề cho bài viết về phim..." />
                        </div>
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Mô Tả Ngắn</label>
                            <textarea v-model="update_bai_viet.mo_ta_ngan" class="form-control" placeholder="Mô tả ngắn về nội dung bài viết" rows="2"></textarea>
                        </div>
                        <div class="col-md-12 mb-3">
                            <label class="form-label">Nội Dung</label>
                            <textarea v-model="update_bai_viet.noi_dung" class="form-control" placeholder="Nội dung chi tiết của bài viết về phim, review, tin tức điện ảnh,..." rows="4"></textarea>
                        </div>
                        <div class="col-md-6 mb-3">
                            <label class="form-label">Hình Ảnh</label>
                            <input v-model="update_bai_viet.hinh_anh" type="text" class="form-control" placeholder="URL hình ảnh minh họa" />
                        </div>
                        <div class="col-md-3 mb-3">
                            <label class="form-label">Tag</label>
                            <input v-model="update_bai_viet.tag" type="text" class="form-control" placeholder="Tag A, Tag B, Tag C"/>
                        </div>
                        <div class="col-md-3 mb-3">
                            <label class="form-label">Trạng Thái</label>
                            <select v-model="update_bai_viet.tinh_trang" class="form-select">
                                <option value="1">Hiển Thị</option>
                                <option value="0">Tạm Tắt</option>
                            </select>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button type="button" class="btn btn-success" data-bs-dismiss="modal" @click="updateBaiViet()">
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
                    <h5 class="modal-title">Xóa Khách Hàng</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="alert alert-warning border-0 bg-warning alert-dismissible fade show py-2">
                        <div class="alert alert-warning border-0 bg-warning alert-dismissible fade show py-2">
                            <div class="d-flex align-items-center">
                                <div class="font-35 text-dark"><i class="bx bx-info-circle"></i>
                                </div>
                                <div class="ms-3">
                                    <h6 class="mb-0 text-dark">Bạn có chắc chắn muốn xóa bài viết
                                        <b>"{{ delete_bai_viet.tieu_de }}"</b>
                                        này không?
                                    </h6>
                                    <div class="text-dark"><b>Lưu ý: </b>Điều này không thể hoàn tác khi nhấn xác nhận
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
                        Đóng
                    </button>
                    <button type="button" class="btn btn-danger" data-bs-dismiss="modal" @click="deleteBaiViet()">
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
            list_bai_viet: [],
            list_tag: [],
            create_bai_viet: {
                tieu_de: '',
                mo_ta_ngan: '',
                noi_dung: '',
                hinh_anh: '',
                tag: '',
                tinh_trang: '',
            },
                update_bai_viet: {
                id: '',
                tieu_de: '',
                mo_ta_ngan: '',
                noi_dung: '',
                hinh_anh: '',
                tag: '',
                tinh_trang: '',
            },
            delete_bai_viet: {
                id: '',
                tieu_de: '',
                mo_ta_ngan: '',
                noi_dung: '',
                hinh_anh: '',
                tag: '',
                tinh_trang: '',
            },
        }
    },
    methods: {
        loadDataBaiViet() {
            axios
                .get('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/bai-viet/get-data')
                .then((res) => {
                    this.list_bai_viet = res.data.data;
                });
        },
        addBaiViet() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/bai-viet/add-data', this.create_bai_viet)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataBaiViet();
                        alert(res.data.message);
                    }
                });
        },
        tagArr(tags) {
            return tags.split(', ');
        },

        updateBaiViet() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/bai-viet/update', this.update_bai_viet)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataBaiViet();
                        alert(res.data.message);
                    }
                });
        },
        deleteBaiViet() {
            axios
                .post('https://be24.deloydz.com/api/39039000-078000-117000-156000/admin/bai-viet/delete', this.delete_bai_viet)
                .then((res) => {
                    if (res.data.status) {
                        this.loadDataBaiViet();
                        alert(res.data.message);
                    }
                });
        },
    },
    mounted() {
        this.loadDataBaiViet();
    },
}
</script>
<style></style>