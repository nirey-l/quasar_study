<template>
    <div class="q-pa-md ">
        <div class="q-gutter-sm q-ma-xl flex-center flex">
            <q-list v-for="(item, i) in items" :key="i" bordered separator class="full-width" >
                <q-item class="row items-center" tag="label">
                    <q-item-section avatar> <!-- avatar: 작은 이미지나 아이콘 등을 위한 섹션을 나타냄 -->
                        <q-checkbox size="xs" v-model="item.checkbox" color="black" />
                    </q-item-section>
                    <q-item-section avatar>
                        <img src="~assets/1.png" class="q-mb-lg" style="max-width: 200px;">
                    </q-item-section>
                    <q-item-section class="column items-center">
                        <div class="text-subtitle1 text-bold">{{ item.name }}</div>
                        <div class="text-subtitle1 text-bold">{{ item.price }}</div>
                    </q-item-section>
                    <q-item-section>
                        <div class="column items-center q-pa-md q-mb-lg">
                            <q-btn flat icon="keyboard_control_key" @click="count = count +1" />
                            <div>
                                {{ count }}
                            </div>
                            <q-btn flat icon="keyboard_arrow_down"  @click="count = count -1" />
                        </div>
                    </q-item-section>
                    <q-item-section>
                        <q-btn flat color="black" label="Remove" @click="removeItem(i)"/>
                    </q-item-section>
                </q-item>
            </q-list>
        </div>

        <div class="row justify-between">
            <div class="q-px-sm q-mt-sm text-h6">
                Your selection is: {{ select }}
            </div>

            <div class="q-px-sm q-mt-sm">
                <q-btn label="Order" color="black" />
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const items = ref([
  { name: "남성 니트", price: "30,000원", checkbox: false, count: 1},
  { name: "남성 니트", price: "30,000원", checkbox: false, count: 1},
  { name: "남성 니트", price: "30,000원", checkbox: false, count: 1}
])
// 선택된 아이템만 필터링
const select = computed(() => {
  return items.value
    .filter(item => item.checkbox) // checkbox가 true인 항목만 필터링
    .map(item => item.name); // 해당 항목의 이름만 추출
});

function removeItem(index) {
  items.value.splice(index, 1); // 해당 인덱스의 아이템을 배열에서 삭제
}

</script>