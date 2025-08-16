<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import axios from 'axios';
const url = 'https://todolist-api.hexschool.io';
const user = ref({
    uid: '',
    nickname: ''
});

const needLogin = ref(true);
const needRegister = ref(false);

const loginField = ref({
    email: '',
    password: ''
});
const login = async() => {
    try{
        console.log(loginField.value);
        const response = await axios.post(`${url}/users/sign_in`, loginField.value);
        document.cookie = `token=${response.data.token}; expires=${new Date(response.data.exp)}; path=/`;
        needLogin.value = false;
        needRegister.value = false;
        alert('status:' + response.data.status);
        window.location.reload();
    }catch(error){
        alert(error.response.data.message);
    }
}
onMounted(async() => {
    const token = document.cookie.replace(/(?:(?:^|.*;\s*)token\s*\=\s*([^;]*).*$)|^.*$/, "$1");
    const response = await axios.get(`${url}/users/checkout`, {
        headers: {
            Authorization: token
        }
    });
    user.value.nickname = response.data.nickname;
    user.value.uid = response.data.uid;
})

const signupField = ref({
    email: '',
    password: '',
    nickname: ''
});
const signup = async() => {
    try{
        console.log(signupField.value);
        const response = await axios.post(`${url}/users/sign_up`, signupField.value);
        needLogin.value = true;
        needRegister.value = false;
        alert('status:' + response.data.status);
    }catch(error){
        alert(error.response.data.message);
    }
}
const logout = () => {
    document.cookie = 'token=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/for-vite-dev-2025';
    setTimeout(() => {
        window.location.reload();
    }, 500);
}
</script>
<template>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <div class="container">
        <h1>HW2</h1>
        <div v-if="user.uid" class="row">
            <div class="col-md-12">
                <h2>登入成功</h2>
                <p>暱稱: {{ user.nickname }}</p>
                <p>uid: {{ user.uid }}</p>
                <button type="button" class="btn btn-light" @click="logout">登出</button>
            </div>
        </div>
        <div v-else class="row">
            <div v-if="needLogin" class="col-md-12">
                <h2>登入</h2>
                <input type="text" class="form-control" placeholder="帳號" v-model="loginField.email">
                <input type="text" class="form-control" placeholder="密碼" v-model="loginField.password">
                <button type="button" class="btn btn-success" @click="login">登入</button>
                <button type="button" class="btn btn-light" @click="needRegister = true; needLogin = false">註冊</button>
            </div>
            <div v-if="needRegister" class="col-md-12">
                <h2>註冊</h2>
                <input type="text" class="form-control" placeholder="帳號" v-model="signupField.email">
                <input type="text" class="form-control" placeholder="密碼" v-model="signupField.password">
                <input type="text" class="form-control" placeholder="暱稱" v-model="signupField.nickname">
                <button type="button" class="btn btn-success" @click="signup">註冊</button>
                <button type="button" class="btn btn-light" @click="needLogin = true; needRegister = false">登入</button>                
            </div>
        </div>
    </div>    
</template>
<style scoped>
    .container{
        text-align: center;
        width: 50%;
    }
    input{
        margin-bottom: 20px;
    }
    .btn{
        margin-right: 10px;
    }
</style>