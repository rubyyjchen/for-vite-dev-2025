<script setup>
import { ref } from 'vue'

const handleClick = () => {
    alert('click')
}

const submitForm = () => {
    alert('submit')
}

const text = ref('一段文字')
</script>
<template>
    <div>
        <br><br><br><br><br><br><br><br><br></br>
        <h2 v-pre>v-on 可監聽事件，可縮寫成 @</h2>
        <h3>.prevent 把預設行為取消</h3>
        <form action="" @submit.prevent="submitForm">
            <button type="button" v-on:click="handleClick">v-on:click</button>
            <button type="button" v-on:click="handleClick">@click</button>
            <button type="submit">submit</button>
        </form>
        <hr>
        <h2>事件修飾符</h2>
        <h3>a href="#" 預設會跳轉頁面的特定id，若沒找到 id 會跳轉到頁面最上方</h3>
        <a href="#" @click="handleClick">click</a>
        <a href="#" @click.prevent="handleClick">click.prevent</a>
        <hr>
        <h2>按鍵修飾符，可指定在哪個按鍵按下去才觸發 v-on:keydown.xxx</h2>
        <input type="text" v-on:keydown.enter="handleClick" v-model="text">v-on:keydown.enter
        <input type="text" @keydown.space="handleClick" v-model="text">@keydown.space
        <br>
    </div>
</template>