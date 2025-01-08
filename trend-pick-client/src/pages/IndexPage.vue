<template>
  <q-page>
    <div class="q-pa-lg q-mb-xs">
      <q-card>
        <q-tabs
          v-model="tab"
          class="bg-black text-bold text-white"
          align="justify"
          narrow-indicator
          style="width: 1570px;"
        >
          <q-tab name="best" label="Best" />
          <q-tab name="new" label="New" />
          <q-tab name="made" label="Made" />
          <q-tab name="discount" label="오늘의 할인" />
          <q-tab name="outer" label="아우터" />
          <q-tab name="dress" label="원피스" />
          <q-tab name="knit" label="니트" />
          <q-tab name="T-shirt" label="티셔츠" />
          <q-tab name="shirt" label="블라우스/셔츠" />
          <q-tab name="skirt" label="스커트" />
          <q-tab name="pants" label="팬츠" />
        </q-tabs>

        <q-separator />

        <q-tab-panels v-model="tab" animated class="bg-grey-4 text-dark text-center" style="width: 1570px;">
          <q-tab-panel name="best">
            아우터   원피스   니트   티셔츠   블라우스/셔츠   스커트   팬츠
          </q-tab-panel>
          <q-tab-panel name="new">
            아우터   원피스   니트   티셔츠   블라우스/셔츠   스커트   팬츠
          </q-tab-panel>
          <q-tab-panel name="made">
            아우터   원피스   니트   티셔츠   블라우스/셔츠   스커트   팬츠
          </q-tab-panel>
          <q-tab-panel name="discount">
            타임세일 45%  1+1  이벤트
          </q-tab-panel>
          <q-tab-panel name="outer">
            자체제작  트위드  패딩  코트  자켓  가디건
          </q-tab-panel>
          <q-tab-panel name="dress">
            자체제작  미니  미디  롱  H라인  A라인 머메이드
          </q-tab-panel>
          <q-tab-panel name="knit">
            자체제작  긴소매  반소매
          </q-tab-panel>
          <q-tab-panel name="T-shirt">
            자체제작  긴소매  반소매 민소매
          </q-tab-panel>
          <q-tab-panel name="shirt">
            자체제작  셔츠  무지  패턴
          </q-tab-panel>
          <q-tab-panel name="skirt">
            자체제작  미니  미디  롱  H라인  A라인 머메이드 프릴
          </q-tab-panel>
          <q-tab-panel name="pants">
            자체제작  반바지  데님  코튼  린넨  슬랙스  스키니
          </q-tab-panel>
        </q-tab-panels>
      </q-card>
    </div>
  
    <div class="q-pa-lg" style="width: 1620px;">
      <div class="row no-wrap shadow-2">
        <q-toolbar class="col-8" :class="$q.dark.isActive ? 'bg-grey-9 text-white' : 'bg-grey-3'">
          <q-btn flat round dense icon="menu" />
          <q-toolbar-title></q-toolbar-title>
          <q-btn flat round dense icon="search" />
        </q-toolbar>
        <q-toolbar class="col-4 bg-black text-white">
          <q-space />
          <q-btn flat round dense icon="Login" @click="Login" />
          <!-- <q-btn flat round dense icon="shopping cart"  /> -->
          <q-btn flat round dense icon="favorite" />
        </q-toolbar>
     </div>
    </div>
  
    <div class="q-mt-lg flex flex-center text-bold text-h2">Trend Pick</div>
    <div class="q-mt-lg flex flex-center">쇼핑몰 소개 문구</div>
  
    <div class="q-pa-lg q-mt-lg">
      <q-carousel
        style="width: 1570px; height: 400px"
        animated
        v-model="slide"
        navigation
        infinite
        :autoplay="autoplay"
        arrows
        transition-prev="slide-right"
        transition-next="slide-left"
        @mouseenter="autoplay = false"
        @mouseleave="autoplay = true"
      >
        <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
        <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
        <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
        <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
      </q-carousel>
  
      <div class="q-mt-xl q-mb-lg flex flex-center text-bold text-h5">New Item</div>
  
      <div class="grid-container" @click="Detail">
        <div class="q-ma-md" v-for="(item, i) in items" :key="i" style="width: 340px;">
          <q-card style="max-width: 350px;" class="my-card" flat bordered>
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
import { ref } from "vue";
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

function Detail() {
  $router.push('detail')
}

function Login() {
  $router.push('login')
}

</script>

<style>
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* 4열 */
  gap: 16px; /* 카드 간의 간격 */
}
</style>
