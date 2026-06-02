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
            </tr>
        </thead>
        <tbody>
            <!-- sau cái dòng lày, chúng ta sẽ sử dụng vòng lặp trong vue để xuất dữ niệu đầy màn hình -->
            <!-- dòng ở dưới nó na ná với for 
             (int vitri = 0; vitri < listBeer.leng - 1, vitri ++) -->
            <tr v-for="(doituong, vitri) in listBeer" :key=doituong.id>
                <td>{{ vitri + 1 }}</td>
                <td>{{ doituong.name }}</td>
                <td>{{ doituong.tuoi }}</td>
                <td>{{ doituong.coc }}</td>
                <td>{{ doituong.sex }}</td>
                <!-- :src ở dưới tức là đang binding (ràng buộc) dữ liệu -->
                <td><img :src=doituong.monan class="rounded" width="20%" heigh="20%" /> </td>
            </tr>
        </tbody>
    </table>
</template>