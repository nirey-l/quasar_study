<template>
    <div class="q-pa-md ">
        <div class="q-gutter-sm q-ma-xl flex-center flex">
            <q-item bordered separator class="full-width" tag="label">
                <q-item-section avatar> <!-- avatar: 작은 이미지나 아이콘 등을 위한 섹션을 나타냄 -->
                    <q-checkbox size="xs" v-model="selectAll" color="black" @click="toggleSelectAll" />
                </q-item-section>
                <q-item-section>
                    <div class="text-bold text-grey-10">전체 선택</div>
                </q-item-section>
                <q-item-section style="max-width: 100px;">
                    <q-btn flat color="black" label="전체 삭제" @click="removeAllItems" />
                </q-item-section>
            </q-item>

            <q-list v-for="(item, i) in items" :key="i" bordered separator class="full-width">
                <q-item class="row items-center" tag="label">
                    <q-item-section avatar> <!-- avatar: 작은 이미지나 아이콘 등을 위한 섹션을 나타냄 -->
                        <q-checkbox size="xs" v-model="item.checkbox" color="black" />
                    </q-item-section>
                    <q-item-section avatar>
                        <img src="~assets/1.png" class="q-mb-lg" style="max-width: 200px;">
                    </q-item-section>
                    <q-item-section class="column q-ml-xl cotent-center">
                        <div class="text-subtitle1 text-bold">{{ item.name }}</div>
                        <div class="text-subtitle1 text-bold">{{ item.price }}</div>
                        <div class="text-subtitle1 text-bold">{{ item.size }}</div>
                    </q-item-section>
                    <q-item-section>
                        <div class="column items-center q-pa-md q-mb-lg">
                            <q-btn flat icon="keyboard_control_key" @click="count = count + 1" />
                            <div>
                                {{ count }}
                            </div>
                            <q-btn flat icon="keyboard_arrow_down" @click="count = count - 1" />
                        </div>
                    </q-item-section>
                    <q-item-section>
                        <q-btn flat color="black" label="Remove" @click="removeItem(i)" />
                    </q-item-section>
                </q-item>
            </q-list>
        </div>

        <div class="row justify-end q-px-sm q-mt-sm">
            <q-btn label="Order" color="black" @click="Index" />
        </div>

        <div>
            <!-- <div class="q-px-sm q-mt-sm text-h6">
                Your selection is: {{ select }}
            </div> -->
        </div>
    </div>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import Cookies from "js-cookie";

const $router = useRouter()
const items = ref([
    { name: "남성 니트", price: "30,000원", checkbox: false, size: "M", count: 1 },
    { name: "남성 니트", price: "30,000원", checkbox: false, size: "M", count: 1 },
    { name: "남성 니트", price: "30,000원", checkbox: false, size: "M", count: 1 }
])
const item = items.value // 해당 상품 객체를 가져옴
const itemId = item.id // 해당 상품의 id 값을 가져옴
const selectAll = ref(false) // 전체 선택 체크박스 상태 관리
const token = ref()

// 선택된 아이템만 필터링
// const select = computed(() => {
//     return items.value
//         .filter(item => item.checkbox) // checkbox가 true인 항목만 필터링
//         .map(item => item.name); // 해당 항목의 이름만 추출
// });

// 전체 선택/해제 기능
function toggleSelectAll() {
    items.value.forEach(item => {
        item.checkbox = selectAll.value // selectAll의 값에 따라 각 항목의 checkbox 상태 변경
    });
}

// 장바구니 상품 전체 삭제
function removeAllItems() {
    items.value = [] // 장바구니에 있는 모든 상품

    api.delete(`/clear`)
        .then((res) => {
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        });
}

// 장바구니 조회
function cart() {
    token.value = Cookies.get('jwt_token')
    console.log(token.value)
    api.get(`/cart`, {
        headers: {
          Authorization: `Bearer ${token.value}`, // JWT 토큰 추가
        }
    })
        .then((res) => {
            items.value = res.data // 받아온 데이터를 items 배열에 저장하여 화면에 표시
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        });
}

// 장바구니 상품 삭제
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

function Index() {
    api.post(`/order/create`)
        .then((res) => {
            console.log(res.data)
        })
        .catch((error) => {
            console.error(error)
        });
    alert("주문이 완료됐습니다");
    $router.push('/')
}

// onMounted: 페이지 처음 로딩시 실행할 코드
onMounted(() => {
    cart();
});

</script>