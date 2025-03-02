<template>
    <div class="q-pa-xl"></div>
    <div class="flex-center flex q-pa-lg">
        <div class="q-pa-lg">
            <div class="text-bold q-mb-lg text-h4">주문 내역</div>
            <div class="row no-wrap shadow-2" style="width: 500px;">
                <q-toolbar class="col bg-grey-3 text-grey-9">
                    <q-toolbar-title>상품명으로 검색하세요</q-toolbar-title>
                    <q-btn flat round dense icon="search" />
                </q-toolbar>
            </div>
            <q-list v-for="(item, i) in items" :key="i">
                <q-card class="my-card q-my-lg" flat bordered>
                    <div class="q-mx-lg q-mt-md text-bold text-h5">{{item.date}}</div>
                    <q-card-section class="row q-py-md">
                        <img src="~assets/1.png" class="q-pa-xs" style="max-width: 200px;">
                        <div class="column content-center">
                            <div class="text-subtitle1 text-bold q-pt-lg q-px-lg">{{ item.name }}</div>
                            <div class="text-subtitle1 text-bold q-pt-sm q-px-lg">{{ item.price }}원</div>
                            <div class="q-pt-sm q-px-lg">{{item.size}} / {{item.count}}개</div>
                            <div class="row q-px-lg q-pt-md">
                                <q-btn color="black" label="배송조회" />
                                <q-btn color="black" label="재구매" class="q-ml-md" />
                            </div>
                        </div>
                    </q-card-section>
                </q-card>
            </q-list>
        </div>
    </div>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref, onMounted } from 'vue';
import Cookies from "js-cookie";

const items = ref([
    { date: "25.02.11", name: "남성 니트", price: "30,000", size: "M", count: 1},
    { date: "25.02.11", name: "남성 니트", price: "30,000", size: "M", count: 1},
    { date: "25.02.11", name: "남성 니트", price: "30,000", size: "M", count: 1}
])

const token = ref()

// 주문 생성
// function createOrder() {
//     api.post(`/order/create`)
//         .then((res) => {
//             console.log(res.data)
//         })
//         .catch((error) => {
//             console.error(error)
//         });
// }

// 사용자 주문 조회
function order() {
    token.value = Cookies.get('jwt_token')
    console.log(token.value)
    api.get(`/order`)
        .then((res) => {
            if (res.status === 200) { //200: http 2xx => 성공
                // 토큰을 쿠키에 저장 (HTTP 전송 시 사용할 수 있도록 설정)
                Cookies.set("jwt_token", res.data.token, {
                    expires: 7, // 7일 동안 유지
                });
                console.log("토큰 저장 완료")
                items.value = res.data // 받아온 데이터를 items 배열에 저장하여 화면에 표시
                console.log(res.data)

            } 
        })
        .catch((error) => {
            console.error(error)
        });
}

onMounted(() => {
    order();
});
</script>