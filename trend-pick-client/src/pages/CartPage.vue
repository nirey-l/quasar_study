<template>
    <div class="q-pa-md ">
        <div class="q-gutter-sm flex-center flex">
            <q-list>
                <q-item tag="label">
                    <q-item-section avatar> <!-- avatar: 작은 이미지나 아이콘 등을 위한 섹션을 나타냄 -->
                        <q-checkbox v-model="order" val="남성 니트" color="black" />
                    </q-item-section>
                    <q-item-section>
                        <img src="~assets/1.png" class="q-mb-lg">
                        <q-item-label class="q-mb-lg flex-center flex text-h5 text-bold">남성 니트</q-item-label>
                    </q-item-section>
                </q-item>
            </q-list>
        </div>

        <!-- <div class="q-px-sm q-mt-sm flex-center flex text-h6">
            Your selection is: <strong>{{ order }}</strong>
        </div> -->

        <div class="q-mt-lg  flex-center flex">
            <q-btn label="Order" color="black" />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const order = ref(null)
</script>