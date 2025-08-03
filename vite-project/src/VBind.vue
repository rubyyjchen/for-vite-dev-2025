<script setup>
import { ref } from 'vue'
const imgUrl = ref('https://images.unsplash.com/photo-1753808645481-070fba323120?q=80&w=350&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D')
const isChecked = ref(false)
</script>
<template>
    <div>
        <h2 v-pre>屬性綁定變數不能用'{{}}'，要用 v-bind</h2>
        <img v-bind:src="imgUrl" alt="random image"></img>
        <h2 v-pre>v-bind:src 可縮寫 :src</h2>
        <img :src="imgUrl" alt="random image"></img>
        <hr>
        <h2 v-pre>v-bind 可綁定在任何屬性上</h2>
        {{ isChecked }}
        <input type="checkbox" v-model="isChecked" />
        <input type="text" v-bind:disabled="isChecked" />
        <input type="text" :disabled="isChecked" />
        <hr>
        <h2 v-pre>v-bind 可套用在行內樣式上，值要是物件形式</h2>
        <div class="box" v-bind:style="{ transform: isChecked ? 'rotate(45deg)' : null }"></div>
        <h3>在 v-bind 遇到 '-' 時，會自動把它轉換成 camelCase 小駝峰</h3>
        <div class="box" :style="{ backgroundColor: isChecked ? 'red' : 'green' }"></div>
        <hr>
        <h2 v-pre>v-bind 可綁定 class，'{ className: 變數}'</h2>
        <div class="box" :class="{ rotate: isChecked }"></div>
    </div>
</template>
<style scoped>
.box {
    background-color: red;
    width: 100px;
    height: 100px;
    transition: all 0.5s;
}
.rotate{
    transform: rotate(45deg);
}
</style>