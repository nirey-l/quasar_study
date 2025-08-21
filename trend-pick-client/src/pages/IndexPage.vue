<template>
  <div>
    <div class="fullscreen-image">
      <div class="overlay-content text-center">
        <h1 class="text-white title-text">NEW SEASON ARRIVALS</h1>
      </div>
    </div>

    <div class="q-pa-xl">
      <div class="text-h5 text-center text-weight-bold q-mb-lg">Best Item</div>
      <div class="row q-col-gutter-lg">
        <div class="col-12 col-sm-6 col-md-3">
          <q-card flat bordered>
            <q-img src="https://i.imgur.com/example1.jpg" />
            <q-card-section>
              <div class="text-subtitle1">클래식 블레이저</div>
              <div class="text-caption text-grey">₩129,000</div>
            </q-card-section>
          </q-card>
        </div>
        <div class="col-12 col-sm-6 col-md-3">
          <q-card flat bordered>
            <q-img src="https://i.imgur.com/example2.jpg" />
            <q-card-section>
              <div class="text-subtitle1">와이드핏 데님 팬츠</div>
              <div class="text-caption text-grey">₩89,000</div>
            </q-card-section>
          </q-card>
        </div>
        <div class="col-12 col-sm-6 col-md-3">
          <q-card flat bordered>
            <q-img src="https://i.imgur.com/example3.jpg" />
            <q-card-section>
              <div class="text-subtitle1">레더 로퍼</div>
              <div class="text-caption text-grey">₩159,000</div>
            </q-card-section>
          </q-card>
        </div>
        <div class="col-12 col-sm-6 col-md-3">
          <q-card flat bordered>
            <q-img src="https://i.imgur.com/example4.jpg" />
            <q-card-section>
              <div class="text-subtitle1">코튼 오버핏 셔츠</div>
              <div class="text-caption text-grey">₩79,000</div>
            </q-card-section>
          </q-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.fullscreen-image {
  /* 👇 height를 min-height로 변경하여 스크롤 가능하게 만듦 */
  min-height: calc(100vh - 66px);
  width: 100%;
  
  background: url('../assets/2.jpeg') no-repeat center center;
  background-size: cover;

  display: flex;
  justify-content: center;
  align-items: center;
}

/* ... 나머지 스타일은 기존과 동일 ... */
.overlay-content {
  z-index: 1;
}

.title-text {
  font-size: 4rem;
  font-weight: 700;
  letter-spacing: 0.2rem;
  margin-bottom: 2rem;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.6);
}

@media (max-width: 600px) {
  .title-text {
    font-size: 2.5rem;
  }
}
</style>