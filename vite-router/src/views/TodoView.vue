<template>
    <h1>Todo API</h1>
    <div>
        <h2>註冊</h2>
        <input type="email" placeholder="帳號" v-model="signupField.email" />
        <input type="text" placeholder="密碼" v-model="signupField.password" />
        <input type="text" placeholder="暱稱" v-model="signupField.nickname" />
        <br/>
        {{ signupField }}
        <br/>
        <button type="button" @click="signup">註冊</button>
        <br/>
        {{ signupResponse }}
    </div>
    <div>
        <h2>登入</h2>
        <input type="email" placeholder="帳號" v-model="loginField.email" />
        <input type="text" placeholder="密碼" v-model="loginField.password" />
        <br/>
        {{ loginField }}
        <br/>
        <button type="button" @click="login">登入</button>
        <br/>
        {{ loginResponse }}
    </div>
    <div>
        <h2>驗證</h2>
        <div v-if="user.uid">
            <p>暱稱: {{ user.nickname }}</p>
            <p>uid: {{ user.uid }}</p>
        </div>
        <div v-else>
            <p>你還沒有登入喔</p>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
const url = 'https://todolist-api.hexschool.io';

const signupField = ref({
    email: '',
    password: '',
    nickname: ''
});
const signupResponse = ref('');
const signup = async() => {
    try{
        const response = await axios.post(`${url}/users/sign_up`, signupField.value);
        console.log(response);
        signupResponse.value = response.data.uid;
    }catch(error){
        console.log(error.response.data.message);
    }
}

const loginField = ref({
    email: '',
    password: ''
});
const loginResponse = ref('');
const login = async() => {
    try{
        const response = await axios.post(`${url}/users/sign_in`, loginField.value);
        console.log(response);
        loginResponse.value = response.data.token;
        document.cookie = `token=${response.data.token}; expires=${new Date(response.data.exp)}; path=/`;
    }catch(error){
        console.log(error.response.data.message);
    }
}

const user = ref({
    nickname: '',
    uid: ''
});
//驗證是否登入要在 onMounted 中執行
onMounted(async() => {
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)token\s*\=\s*([^;]*).*$)|^.*$/, "$1");
    console.log(token);
    const response = await axios.get(`${url}/users/checkout`, {
        headers: {
            Authorization: token
        }
    });
    console.log(response);
    user.value.nickname = response.data.nickname;
    user.value.uid = response.data.uid;
})
</script>

<style>

</style>