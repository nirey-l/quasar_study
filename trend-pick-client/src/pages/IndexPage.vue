<template>
  <q-page style="padding: 0;">
    <div class="main-banner">
      <q-img 
        src="~assets/main.jpeg" 
        style="min-height: 60vh;" 
        fit="cover"
      >
        <div class="absolute-full flex flex-center">
          <h1 class="text-white title-text">NEW SEASON ARRIVALS</h1>
        </div>
      </q-img>
    </div>

    <div class="row">
      <div class="col-6 cursor-pointer" @click="goToPage('/collection')">
        <q-img src="~assets/main2.jpeg" :ratio="1">
          <div class="absolute-full flex flex-center">
            <h2 class="text-white subtitle-text">Collection</h2>
          </div>
        </q-img>
      </div>
      <div class="col-6 cursor-pointer" @click="goToPage('/shop')">
        <q-img src="~assets/main3.jpeg" :ratio="1">
          <div class="absolute-full flex flex-center">
            <h2 class="text-white subtitle-text">Shop</h2>
          </div>
        </q-img>
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

// 페이지 이동 함수
function goToPage(path) {
  router.push(path);
}
</script>

<style scoped>
.title-text {
  font-size: 3rem;
  font-weight: 700;
  letter-spacing: 0.2rem;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.6);
}

/* 👇 작은 이미지 위의 텍스트를 위한 새로운 스타일 */
.subtitle-text {
  font-size: 2rem;
  font-weight: 600;
  letter-spacing: 0.1rem;
  text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.7);
}

/* 이미지 아래의 작은 공백 제거 */
.q-img {
  vertical-align: top;
}

/* 모바일 화면 대응 */
@media (max-width: 600px) {
  .title-text {
    font-size: 1.8rem;
  }
  .subtitle-text {
    font-size: 1.2rem;
  }
}
</style>