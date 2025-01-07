<template>
  <div class="q-pa-lg">
    <q-btn-toggle
      v-model="model"
      toggle-color="white"
      color="black"
      style="width: 1570px; height: 200"
      :options="[
        {label: 'Best', value: 'best', style: 'width: 145px;'},
        {label: 'New', value: 'new', style: 'width: 145px;'},
        {label: 'Made', value: 'made', style: 'width: 145px;'},
        {label: '오늘의할인', value: 'discount', style: 'width: 145px;'},
        {label: '아우터', value: 'outer', style: 'width: 145px;'},
        {label: '원피스', value: 'dress', style: 'width: 140px;'},
        {label: '니트', value: 'knit', style: 'width: 140px;'},
        {label: '티셔츠', value: 't-shirt', style: 'width: 140px;'},
        {label: '블라우스/셔츠', value: 'shirt', style: 'width: 145px;'},
        {label: '스커트', value: 'skirt', style: 'width: 140px;'},
        {label: '팬츠', value: 'pants', style: 'width: 140px;'},
      ]"
    />
  </div>

  <div class="q-pa-lg" style="width: 1570px;">
    <div class="row no-wrap shadow-2">
      <q-toolbar class="col-8" :class="$q.dark.isActive ? 'bg-grey-9 text-white' : 'bg-grey-3'">
        <q-btn flat round dense icon="menu" />
        <q-toolbar-title></q-toolbar-title>
        <q-btn flat round dense icon="search" />
      </q-toolbar>
      <q-toolbar class="col-4 bg-black text-white">
        <q-space />
        <!-- <q-btn flat round dense icon="shopping cart"  /> -->
        <q-btn flat round dense icon="favorite" />
      </q-toolbar>
   </div>
  </div>

  <q-page class="q-pa-lg">
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

    <div class="q-ma-xl">
      <q-card style="max-width: 350px;" class="my-card" flat bordered>
        <img src="~assets/1.png">
        <div class="row justify-between items-center q-pa-md">
          <div>
            <div class="text-bold">남성 니트</div>
            <div>30,000원</div>
          </div>
        <q-card-actions align="right">
          <q-btn flat round color="red" icon="favorite" />
          <q-btn flat round color="primary" icon="share" />
        </q-card-actions>
        </div>
      </q-card>
    </div>
    <div class="q-ma-xl">
      <q-card style="max-width: 350px;" class="my-card" flat bordered>
        <img src="~assets/1.png">
        <div class="row justify-between items-center q-pa-md">
          <div>
            <div class="text-bold">남성 니트</div>
            <div>30,000원</div>
          </div>
        <q-card-actions align="right">
          <q-btn flat round color="red" icon="favorite" />
          <q-btn flat round color="primary" icon="share" />
        </q-card-actions>
        </div>
      </q-card>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
const autoplay = ref(true) //캐러셀은 초기 상태에서 자동 재생
</script>
