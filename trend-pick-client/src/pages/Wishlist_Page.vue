<template>
    <div class="q-my-xl flex flex-center text-bold text-h4">Whish List</div>
    <div class="row">
        <div class="q-mx-lg q-mb-xl " v-for="(item, i) in items" :key="i" style="width: 340px;">
            <q-card style="max-width: 350px;" class="my-card cursor-pointer" flat bordered>
                <img src="~assets/1.png" @click="Detail(item.id)">
                <div class="row justify-between items-center q-pa-md">
                    <div>
                        <div class="text-bold">{{ item.name }}</div>
                        <div>{{ item.price }}</div>
                    </div>
                    <q-card-actions align="right">
                        <q-btn flat round icon="delete" @click="removeItem(i)" />
                    </q-card-actions>
                </div>
            </q-card>
        </div>
    </div>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router"; // route: 페이지 url, router: 라우팅

const $router = useRouter()
const items = ref([
    { id: 1, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
    { id: 2, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
    { id: 3, image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
])
const item = items.value // 해당 상품 객체를 가져옴
const itemId = item.id // 해당 상품의 id 값을 가져옴

// 상품 상세 페이지 이동
function Detail(itemId) {
    api.get(`/item/${itemId}`)
        .then((res) => {
            console.log(res.data)
            $router.push(`detail?itemId=${itemId}`)
        })
        .catch((error) => {
            console.error(error)
        });
}

// 사용자 위시리스트 조회
function wishlist() {
    api.get(`/wishlist`)
        .then((res) => {
            items.value = res.data // 받아온 데이터를 items 배열에 저장하여 화면에 표시
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        });
}

// 위시리스트 상품 삭제
function removeItem(index) {
    items.value.splice(index, 1); // 해당 인덱스의 아이템을 배열에서 삭제

    api.delete(`/remove/${itemId}`)
        .then((res) => {
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        });
}

// onMounted: 페이지 처음 로딩시 실행할 코드
onMounted(() => {
    wishlist();
});

</script>