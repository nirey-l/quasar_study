<template>
    <q-page class="flex-center flex">
        <div class="q-pa-md" style="max-width: 400px">
            <div class="text-bold q-mb-lg text-h6">로그인</div>
            <div class="q-gutter-md">
                <q-input filled v-model="id" label="id" lazy-rules
                    :rules="[val => val && val.length > 0 || 'Please type something']" />

                <q-input filled type="password" v-model="pwd" label="password" lazy-rules :rules="[
                    val => val !== null && val !== '' || 'Please type your password',
                ]" />

                <div class="column q-gutter-y-md">
                    <q-btn @click="Login" label="Login" type="submit" color="primary" />
                    <q-btn @click="Signup" label="Signup" type="submit" color="primary" to="/signup" />
                </div>
            </div>
        </div>
    </q-page>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const id = ref()
const pwd = ref()
const data = ref({})
const $router = useRouter()

function Login() {
    data.value.id = id.value
    data.value.pw = pwd.value
    console.log(data.value)
    //실제 로그인 요청 보내기
    $router.push('/')
}
</script>