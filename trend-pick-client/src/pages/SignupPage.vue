<template>
    <q-page class="flex-center flex">
        <div class="q-pa-md" style="max-width: 400px">
            <div class="text-bold q-mb-lg text-h6">회원가입</div>
            <div class="q-gutter-xs">
                <q-input filled v-model="name" label="name" lazy-rules
                    :rules="[val => val && val.length > 0 || 'Please type something']" />
                <div class="row items-center">
                    <q-input filled v-model="id" label="id/e-mail" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']">
                        <template v-slot:append>
                            <q-btn label="중복확인" type="submit" color="primary" class="q-my-xs" />
                        </template>
                    </q-input>

                </div>

                <q-input filled type="password" v-model="pwd" label="password" lazy-rules :rules="[
                    val => val !== null && val !== '' || 'Please type your password',
                ]" />
                <q-input filled type="password" v-model="checkPwd" label="재입력" lazy-rules :rules="[
                    val => val !== null && val !== '' || 'Please type your password',
                ]" />

                <div class="column q-gutter-y-md">
                    <q-btn @click="Signup" label="Signup" type="submit" color="primary" />
                </div>
            </div>
        </div>
    </q-page>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const $router = useRouter()
const name = ref()
const id = ref()
const pwd = ref()
const checkPwd = ref()
const data = ref()

function Signup() {
    if (pwd.value===checkPwd.value) {
        data.value = {
            nickName: name,
            email: id,
            password : pwd
        }
        console.log(data.value)
        $router.push('/')
    }
    else {
        alert("비밀번호가 일치하지 않습니다")
    }
}
</script>