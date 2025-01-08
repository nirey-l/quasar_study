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
        
        <!-- <div class="q-pa-xl content-center justify-center" style="max-width: 500px;">
            <q-carousel
                swipeable
                animated
                v-model="slide"
                thumbnails
                infinite
        >
            <q-carousel-slide :name="1" img-src="~assets/1.png" />
            <q-carousel-slide :name="2" img-src="https://cdn.quasar.dev/img/parallax1.jpg" />
            <q-carousel-slide :name="3" img-src="https://cdn.quasar.dev/img/parallax2.jpg" />
            <q-carousel-slide :name="4" img-src="https://cdn.quasar.dev/img/quasar.jpg" />
            </q-carousel>
        </div> -->

        <div class="q-ma-xl">
            <div class="text-bold q-mb-md text-h5">남성 니트</div>
            <div class="text-bold q-mb-md text-h6">30,000원</div>
            <div class="q-mb-xs text-h7">사이즈</div>
            <q-btn class="q-mb-lg" label="Free" type="submit" color="black" />
            <div class="q-mb-xs text-h7">수량</div>
            <q-btn class="q-mb-xl" label="Free" type="submit" color="black" />
            <div class="text-bold q-mb-lg text-h6">총금액</div>
        </div>
    </q-page>
</template>

<script setup>
//import { ref } from "vue";

//const slide = ref(1) //첫 번째 슬라이드가 초기 상태에서 표시
</script>