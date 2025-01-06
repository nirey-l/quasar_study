<template>
    <q-page>
        <div class="q-pa-md">
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

        <div class="q-pa-xl"></div>

        <div class="flex flex-center">
            <div class="q-pa-md" style="max-width: 400px">
                <div class="text-bold q-mb-lg text-h4">Sign-up</div>
                <div class="q-gutter-xs">
                    <q-input filled v-model="name" label="name" lazy-rules
                        :rules="[val => val && val.length > 0 || 'Please type something']" />
                    <div class="row items-center">
                        <q-input filled v-model="id" label="id/e-mail" lazy-rules
                            :rules="[val => val && val.length > 0 || 'Please type something']">
                            <template v-slot:append>
                                <q-btn label="중복확인" type="submit" color="black" class="q-my-xs" />
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
                        <q-btn @click="Signup" label="Signup" type="submit" color="black" />
                    </div>
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