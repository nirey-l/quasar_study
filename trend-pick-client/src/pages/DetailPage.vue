<template>
    <q-page class="row items-center justify-between q-pa-xl">
        <div class="col ">
            <q-carousel swipeable animated v-model="slide" thumbnails infinite>
                <q-carousel-slide :name="1" img-src="~assets/1.png" />
                <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
                <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
                <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
            </q-carousel>
        </div>

        <div class="col-4 column content-center">
            <div class="text-bold q-mb-md text-h5">남성 니트</div>
            <div class="text-bold q-mb-md text-h6">{{ price }}원</div>

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
            <q-btn label="Shopping cart" color="black" @click="Cart" />
        </div>
    </q-page>
</template>

<script setup>
import { onMounted, ref, computed } from 'vue';
import { useRoute } from 'vue-router';
import { useRouter } from "vue-router";

const productId = ref()
const $route = useRoute()
const $router = useRouter()
const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
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