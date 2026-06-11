<script setup>
// dòng ở dưới, chúng ta sử dụng Props để tiến hành ràng buộc dữ liệu giữa component cha và con
// Table.vue sẽ đóng vai trò là component con, còn component cha là bất cứ component nào gọi nó
// và truyền cái biến listBeer đã định nghĩa ở dưới
const props = defineProps({
    listBeer: {
        type: Array
    },
    ten: {
        type: String
    }
})
// chúng ta đã học defineProps là bắn từ cha về con, bây giờ sẽ học defineEmits để bắn ngược lại
// từ con -> cha
const emits = defineEmits(["remove", "update", "detail"]) // dòng này tức là tạo 1 emits chứa 2 sự kiện đó là remove và sửa

const xoa = (vitri) => {
    if (confirm("Mày có chắc chắn muốn xoá món ăn thứ " + (vitri + 1) + " không ?")) {
        emits("remove", { vitri }) // dòng này tức là thằng con bắn 1 sự kiện về phía cha,
        // sự kiện có tên là remove, và đính kèm vị trí cần xoá tới thằng cha
    }
}

// cái hàm ở dưới, dùng để mỗi lần click vào 1 dòng -> truyền cái vị trí của dòng đó tới component cha
const detail = (vitri) => {
    emits("detail", { vitri })
}
</script>
<template>
    <p class="text-danger">Đây là biến tạo ở props và truyền từ component cha, có nội
        dung là {{ ten }}</p>
    <!-- Kiến thức về table -->
    <table class="table table-bordered table-striped table-hover">
        <thead>
            <tr>
                <th>STT</th>
                <th>Tên</th>
                <th>Tủi</th>
                <th :class="bien5">Uống bao nhiêu cốc</th> <!-- :class ở đây là binding class  -->
                <th :style="bien6">Sex 🙅🙅🙅🙅</th> <!-- :style ở đây là binding style -->
                <th>Món ưa thích</th>
                <th>Hành động 🤦🏻‍♂️🤦🏻‍♂️🤦🏻‍♂️🤦🏻‍♂️</th>
            </tr>
        </thead>
        <tbody>
            <!-- sau cái dòng lày, chúng ta sẽ sử dụng vòng lặp trong vue để xuất dữ niệu đầy màn hình -->
            <!-- dòng ở dưới nó na ná với for 
             (int vitri = 0; vitri < listBeer.leng - 1, vitri ++) -->
            <tr v-for="(doituong, vitri) in listBeer" :key=doituong.id @click="detail(vitri)">
                <td>{{ vitri + 1 }}</td>
                <td>{{ doituong.name }}</td>
                <td>
                    <!-- dưới đây là kiến thức về if-else, khi đi thi có thể 
                     sẽ có bài về hiển thị 1 cái ô dữ liệu nào đó theo điều kiện bất kỳ
                     và đây là kiến thức thêm để lấy 10đ, chứ không liên quan tới luồng
                     CRUD bình thường. Ngoài ra, còn 1 thuộc tính nữa v-show, nó cũng 
                     xử lý hiển thị nhưng khác v-if ở chỗ đó là thành phần được hiển thị
                     chỉ bị ẩn đi chứ không mất hẳn như v-if. Mọi người có thể tìm hiểu
                     thêm về v-show (cơ chế hoạt động của v-show đó là display: none) -->
                    <p v-if="doituong.tuoi < 5">
                        Trẻ con có tuổi là
                    </p>
                    <p v-else-if="doituong.tuoi > 5 && doituong.tuoi <= 18">
                        Thanh niên có tuổi là
                    </p>
                    <p v-else>
                        Đây là người lớn có tuổi là
                    </p>
                    {{ doituong.tuoi }}
                </td>
                <td>{{ doituong.coc }}</td>
                <td>{{ doituong.sex }}</td>
                <!-- :src ở dưới tức là đang binding (ràng buộc) dữ liệu -->
                <td><img :src=doituong.monan class="rounded" width="20%" heigh="20%" /> </td>
                <td>
                    <button class="btn btn-danger btn-outline-danger text-info" type="button" @click="xoa(vitri)">
                        Xoá
                    </button>
                </td>
            </tr>
        </tbody>
    </table>
</template>