<template>
  <q-page>

    <div class="q-pa-lg" >
      <div class="row no-wrap shadow-2">
        <q-toolbar class="col" :class="$q.dark.isActive ? 'bg-black text-white' : 'bg-grey-3'">
          <q-btn flat round dense icon="menu" />
          <q-toolbar-title></q-toolbar-title>
          <q-btn flat round dense icon="search" />
        </q-toolbar>
      </div>
    </div>

    <div class="q-mt-lg flex flex-center text-bold text-h2">Trend Pick</div>
    <div class="q-mt-lg flex flex-center">쇼핑몰 소개 문구</div>

    <div class="q-pa-lg q-mt-lg">
      <q-carousel style="height: 400px" animated v-model="slide" navigation infinite :autoplay="autoplay"
        arrows transition-prev="slide-right" transition-next="slide-left" @mouseenter="autoplay = false"
        @mouseleave="autoplay = true">
        <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
        <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
        <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
        <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
      </q-carousel>

      <div class="q-mt-xl q-mb-lg flex flex-center text-bold text-h5">New Item</div>

      <div class="row" >
        <div class="q-mr-lg q-mb-xl " v-for="(item, i) in items" :key="i" style="width: 340px;">
          <q-card @click="Detail(i)" style="max-width: 350px;" class="my-card cursor-pointer" flat bordered>
            <img src="~assets/1.png">
            <div class="row justify-between items-center q-pa-md">
              <div>
                <div class="text-bold">{{ item.name }}</div>
                <div>{{ item.price }}</div>
              </div>
              <q-card-actions align="right">
                <q-btn flat round color="red" icon="favorite" />
                <q-btn flat round color="primary" icon="share" />
              </q-card-actions>
            </div>
          </q-card>
        </div>
      </div>

      <div class="q-mt-xl q-mb-lg flex flex-center text-bold text-h5">Weekly Best</div>
    </div>
  </q-page>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router"; 
const $router = useRouter()
const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
const autoplay = ref(true) //캐러셀은 초기 상태에서 자동 재생
const items = ref([
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" },
  { image: "~assets/1.png", name: "남성 니트", price: "30,000원" }
])

function Detail(index) {
  console.log(index)
  $router.push(`detail?itemId=${index}`)
}

onMounted(()=>{
})
</script>
