<script setup>
import { reactive, ref } from 'vue'; // đây là 1 công cụ trong vue giúp chúng ta quản lý dữ liệu
import Table from './Table.vue';
// quản lý thì bao gồm là tạo, sửa và xuất ra màn hình

// tạo thử 1,2 biến với cái ref trên kia
const bien1 = ref('Nông Văn Hùng dân trơi') // tạo biến ref quản lý 1 ô nhớ kiểu String
const tuoiCuaThangHung = ref(18) // tạo biến ref quản lý 1 ô nhớ kiểu Number
const bien3 = ref(false) // tạo biến ref quản lý 1 ô nhớ kiểu Bool

// sau khi có 3 biến bên trên, thử xuất ra màn hình với interpolation (lội xuy)
// cái nội suy kia có thể gọi tên khác là binding (ràng buộc) 1 chiều, ở đây là chiều
// từ controller (file xử lý, trong cặp script) tới view (màn hình)
// binding tức là ở controller thay đổi thì ở bên view phải thay đổi theo
// nhưng 1 chiều tức là chỉ controller tới view thôi, còn từ view thay đổi thì 
// controller không thay đổi theo

// 1 kiểu binding nữa ngoài nội suy
// binding class,style, các thẻ thuộc tính của HTML như width, height,...
// cú pháp là vẫn viết style, class như bình thường, nhưng NHỚ nà phải có dấu :,
// ví dụ :style, :class,...
const bienStyle = { 'color': 'red' }

// Đây là ví dụ về biến ref với kiểu dữ liệu là Array
const tenList = ref(
    [
        {
            id: 2,
            ten: "abc",
            tuoi: 20,
            conSongKhong: true
        },
        {
            id: 3,
            ten: "abcd",
            tuoi: 30,
            conSongKhong: true
        }
    ]
)
const listBeer = ref(
    [
        {
            id: 1,
            name: "Bách",
            tuoi: 4,
            monan: "https://cdn2.fptshop.com.vn/unsafe/1920x0/filters:format(webp):quality(75)/mon_nhau_don_gian_21775cd4c5.png",
            coc: 20,
            sex: "nam"
        },
        {
            id: 2,
            name: "Nam",
            tuoi: 12,
            monan: "https://static-images.vnncdn.net/vps_images_publish/000001/000003/2024/9/25/cach-lam-dau-phu-tam-hanh-ngon-don-gian-tai-nha-4855.jpg?width=1200&s=FJsEs6saBgRmjqI6MLDbAQ",
            coc: 30,
            sex: "nam"
        },
        {
            id: 3,
            name: "Chiến",
            tuoi: 25,
            monan: "https://imgs.vietnamnet.vn/Images/2017/10/09/16/20171009163405-long-ga-trung-non-chay-toi.jpg?width=0&s=mkDMCmLU5iKvuhsT-FdLwg",
            coc: 20,
            sex: "nữ"
        },
    ]
)
// cái biến doituong ở dưới, sẽ dùng để hứng (hoặc để lưu) các giá trị của cái form trên màn hình
// cái reactive ở dưới tương tự với ref nhưng ngắn gọn hơn -> 2 cái gần như tương tự nhau về chức năng
const doituong = reactive(
    {
        id: Math.random,
        name: "",
        tuoi: 0,
        monan: "",
        coc: 0,
        sex: ""
    }
)

const bien5 = ref('text-primary') // String
const bien6 = 'font-size: 20px' // String
const bien7 = ref(7) // Number

const doimauxanh = () => {
    bien5.value = "text-success"
}

const doimauvang = () => {
    bien5.value = "text-warning"
}
const bienten = ref("Khủng long")

const dangky = () => {
    // nếu là update thì update, ở dứoi phải có .value là bởi vì biến kiểu ref, muốn truy xuất phải dùng .value
    // còn nếu biến kiểu reactive thì không cần .value. Trong cái môn này, anh em dùng ref hay reactive được hết
    // cái nào anh em thích thì dùng
    if (isUpdate.value) {
        // bắt cái thằng có id trùng với id cần update
        let doiTuongCanUpdate = listBeer.value.find(beer => beer.id === doituong.id)

        // sau khi bắt được, chúng ta tiến hành update
        doiTuongCanUpdate.name = doituong.name,
            doiTuongCanUpdate.tuoi = doituong.tuoi,
            doiTuongCanUpdate.monan = doituong.monan,
            doiTuongCanUpdate.coc = doituong.coc,
            doiTuongCanUpdate.sex = doituong.sex
        //sau khi sửa xong, reset lại form cho chắc cú, đỡ bị update hoặc thêm mới trùng
        resetForm()

    }
    // nếu không thì thêm mới
    else {
        // sau khi click đăng ký, thì chúng ta sẽ thêm doituong vào list đang hiển thị dữ liệu ở bảng -> luồng 6,7 điểm thêm mới
        listBeer.value.unshift(
            { ...doituong }
        )
        // sau khi thêm mới, reset lại cái form
        doituong.id = Math.random,
            doituong.name = "",
            doituong.tuoi = 0,
            doituong.monan = "",
            doituong.coc = 0,
            doituong.sex = ""
    }

}
// Kiến thức để lấy 5 điểm trong môn vue, đó là tạo Array chứa dữ liệu, sau đó 
// xuất ra table

const xoa = (vitri) => {
    // bắt đầu xoá
    listBeer.value.splice(vitri.vitri, 1)
}
const isUpdate = ref(false) // ban đầu là chưa update, nên cái cờ này được đặt là false
const xem = (vitri) => {
    // từ cái vị trí thu được, tìm trong mảng và lôi nó ra
    let doiTuongTimDuoc = { ...listBeer.value[vitri.vitri] }
    // mỗi lần click xem, thì ta đổi cái cờ update thành true
    isUpdate.value = true
    doituong.id = doiTuongTimDuoc.id,
        doituong.name = doiTuongTimDuoc.name,
        doituong.tuoi = doiTuongTimDuoc.tuoi,
        doituong.monan = doiTuongTimDuoc.monan,
        doituong.coc = doiTuongTimDuoc.coc,
        doituong.sex = doiTuongTimDuoc.sex
}

// mỗi lần reset form, thì tất các trường reset lại, bao gồm cả cái cờ update kia
const resetForm = () => {
    doituong.id = Math.random,
        doituong.name = "",
        doituong.tuoi = 0,
        doituong.monan = "",
        doituong.coc = 0,
        doituong.sex = ""
    isUpdate.value = false
}
</script>
<!-- Mọi code html phải đặt ở trong cái thẻ template này thì 
 giao diện mới hiện ra -->
<template>
    <div>
        <!-- text-center căn lề giữa 
         bg-success: background màu xanh-->
        <div class="text-center bg-success">
            <h2 class="text-danger">Tôi muốn bỏ học</h2>
            <!-- text-danger ở trên có nghĩa là cho chữ thành màu đỏ, nó tương ứng với color: red
         các màu sắc cần nhớ:
         danger: đỏ
         success: xanh
         warning: vàng
         và 1 số màu khác như là primary, secondary, light, info
         cách sử dụng: text-info, text-warning, text-success -->
            <h2 class="text-primary">Tôi yêu thầy</h2>
            <h2 class="text-warning">Tôi thích bơi here</h2>
            <h2 class="text-light">Uy tín luôn</h2>
        </div>

    </div>

    <div class="row">
        <div class="col-6">
            <!-- kiến thức về form, fw-bold: lm cho chữ đậm lên -->
            <form class="form" @reset="resetForm">
                <div class="d-flex mb-4">
                    <label class="form-label fw-bold" style="margin-right: 2em;">Tên</label>
                    <!-- cái v-model ở dưới là kỹ thuật binding (ràng buộc) 2 chiều,
                     tức là ở view thay đổi thì bên js nhận được, hoặc js thay đổi thì view hiển thị
                     tương ứng -->
                    <input type="text" class="form-control w-50 ms-4" v-model="doituong.name">
                </div>
                <div class="d-flex gap-4">
                    <label class="form-label fw-bold" style="margin-right: 2em;">Tuổi</label>
                    <input type="number" class="form-control w-50" v-model="doituong.tuoi">
                </div>
                <div class="d-flex gap-4">
                    <label class="form-label fw-bold" style="margin-right: 2em;">mày uống bao nhiêu</label>
                    <select class="form-select w-50" v-model="doituong.coc">
                        <option value="0">--- Mời chọn cốc ---</option>
                        <option value="1">1 cốc</option>
                        <option value="10">10 cốc</option>
                        <option value="20">20 cốc</option>
                        <option value="30">30 cốc</option>
                        <option value="999">Bất tử</option>
                    </select>
                </div>
                <div class="d-flex gap-4" mb-4>
                    <label class="form-label fw-bold" style="margin-right: 2em;">mày giới tình gì</label>
                    <input type="radio" name="gioitinh" value="nam" v-model="doituong.sex">
                    <label class="form-label fw-bold" style="margin-right: 2em;">nam</label>
                    <input type="radio" name="gioitinh" value="nữ" v-model="doituong.sex">
                    <label class="form-check-label">Gái</label>

                </div>
                <div class="mb-4">
                    <label class="form-label fw-bold" style="margin-right: 2em;">Thích ăn món gì</label>
                    <input type="text" class="form-control w-50 ms-4" name="monanuathich" v-model="doituong.monan" />
                    <!-- kiến thức về btn -->
                </div>
                <button :class='isUpdate ? "btn btn-danger" : "btn btn-success"' type="submit"
                    @click.prevent="dangky()">
                    {{ isUpdate ? "Tao sửa tí" : "Chốt, t đki" }}
                </button>
                <button class="btn btn-warning" type="reset">Vợ chưa cho</button>
                <button class="btn btn-success" type="button">Đây là btn</button>
            </form>
        </div>
        <div class="col-6"></div>
    </div>
    <!-- Chúng ta sẽ gọi Table.vue sau dòng này -->
    <!-- cái :listBeer tức là HelloWorld đang là component cha, gọi thằng Table là component
      con, và truyền vào biến listBeer tới biến listBeer đã định nghĩa ở trong component con -->
    <!-- ở dưới đoạn @remove tức là thằng cha hứng cái sự kiện xoá từ thằng con -->
    <Table :listBeer=listBeer :ten=bienten @remove="xoa" @detail="xem" />
</template>
