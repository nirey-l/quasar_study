<template>
    <q-page class="row items-center justify-between q-pa-xl">
        <div class="col ">
            <q-carousel swipeable animated v-model="slide" thumbnails infinite>
            <!-- swipeable: 사용자가 슬라이드를 터치로 전환 가능, animated: 애니메이션 효과를 활성화, v-model="slide": 현재 표시 중인 슬라이드의 상태를 관리하는 변수, thumbnails: 아래에 작은 썸네일 이미지를 표시, infinite: 마지막 슬라이드에서 처음 슬라이드로 계속 순환 -->
                <q-carousel-slide :name="1" img-src="~assets/1.png" />
                <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
                <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
                <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
            </q-carousel>
        </div>

        <div class="col-4 column content-center">
            <div class="text-bold q-mb-md text-h5">{{ name }}</div>
            <div class="text-bold q-mb-md text-h6">{{ price }}원</div>
            <!-- {{ price }}는 Vue의 데이터 바인딩을 이용해 price 값을 표시 -->

            <div class="q-mb-xs text-h7 text-bold">사이즈</div>
            <q-btn v-if="isFreesize" class="q-mb-lg" label="Free" type="submit" color="black" />
            <q-btn-group v-else class="q-mb-lg">
                <q-btn label="XS" type="submit" color="black" />
                <q-btn label="S" type="submit" color="black" />
                <q-btn label="M" type="submit" color="black" />
                <q-btn label="L" type="submit" color="black" />
                <q-btn label="XL" type="submit" color="black" />
            </q-btn-group>
 
            <div class="q-mb-xs text-h7 text-bold">수량</div>
            <div class="q-pa-md q-mb-lg">
                <q-input v-model="quantity" type="number" filled />
            </div>
            <div class="text-bold q-mb-lg text-h6">총금액</div>
            <div class="text-bold q-mb-lg text-h6">{{ totalPrice }}원</div>
            <!-- Vue의 computed를 통해 계산된 totalPrice 값을 실시간 표시 -->
            <q-btn label="Shopping cart" color="black" @click="Cart" />
        </div>
    </q-page>
</template>

<script setup>
import { onMounted, ref, computed } from 'vue';
import { useRoute } from 'vue-router'; //route: 페이지 url
import { useRouter } from "vue-router"; //router: 라우팅 


const productId = ref()
const $route = useRoute()
const $router = useRouter()
const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
const name = "남성 니트"
const price = 30000
const quantity = ref(1)
const totalPrice = computed(() => price*quantity.value) //computed(): 이미 ref로 선언된 값에 따라 또 바껴야 하는 변수
const isFreesize = ref(false)

// axios.get('getProduct?')

onMounted(() => {
    console.log($route.query.itemId)
    productId.value = $route.query.itemId
})

function Cart() {
    $router.push('cart')
}
</script>