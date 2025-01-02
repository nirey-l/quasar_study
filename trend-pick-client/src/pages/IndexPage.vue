<template>
  <q-page class="q-pa-lg">
    <q-carousel
      animated
      v-model="slide"
      arrows
      navigation
      infinite
    >
      <q-carousel-slide :name="1" img-src="https://cdn.quasar.dev/img/mountains.jpg" />
      <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
      <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
      <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
    </q-carousel>

    <q-card style="max-width: 240px;" class="my-card" flat bordered>
      <img src="~assets/1.png">

      <div class="row justify-between items-center q-pa-md">
        <div>
          <div>남성 니트</div>
          <div>30,000원</div>
        </div>
        
        <q-card-actions align="right">
          <q-btn flat round color="red" icon="favorite" />
          <q-btn flat round color="primary" icon="share" />
        </q-card-actions>
      </div>

    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
const slide = ref(1)
</script>
