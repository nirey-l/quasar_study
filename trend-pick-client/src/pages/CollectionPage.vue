<template>
  <q-page class="q-pa-md">
    <!-- 컬렉션 소개 섹션 -->
    <div class="collection-header text-center q-my-xl">
      <!-- 작은 부제 -->
      <p class="text-h6 text-grey-6">
        Trend Pick 2025 Fall Collection
      </p>
      <!-- 메인 타이틀 -->
      <h2 class="text-h2 text-weight-light q-my-lg main-title">
        'Modern Classic'
      </h2>
      <!-- 간단한 소개글 -->
      <p class="text-subtitle1 text-grey-8 q-mt-xl">
        시간을 초월하는 클래식의 본질을 현대적인 감각으로 재해석하여, 절제된 우아함과 세련된 실루엣을 선보입니다.
      </p>
    </div>

    <!-- 컬렉션 이미지 리스트 (2열 그리드) -->
    <div class="row q-col-gutter-md q-mt-xl">
      <div class="col-12 col-sm-6 q-mt-lg">
        <q-img src="~assets/collection1.jpeg" :ratio="4/5" />
      </div>
      <div class="col-12 col-sm-6 q-mt-lg">
        <q-img src="~assets/collection4.jpeg" :ratio="4/5" />
      </div>
      <div class="col-12 col-sm-6">
        <q-img src="~assets/collection3.jpeg" :ratio="4/5" />
      </div>
      <div class="col-12 col-sm-6">
        <q-img src="~assets/collection2.jpeg" :ratio="4/5" />
      </div>
    </div>
  </q-page>
</template>

<script setup>
// 이 페이지는 정적인 콘텐츠를 보여주므로 별도의 스크립트 로직이 필요 없습니다.
</script>

<style scoped>
.collection-header {
  max-width: 800px; /* 너비를 조금 더 넓혀 전체적인 균형을 맞춥니다. */
  margin-left: auto;
  margin-right: auto;
}

.main-title {
  font-family: 'Times New Roman', Times, serif; /* 세리프 폰트로 클래식한 느낌을 줍니다. */
  letter-spacing: 2px;
}

.q-img {
  vertical-align: top;
}
</style>
