<script setup>
// 這個 setup 等同於在元件裡寫的 setup 函式
// 區塊裡寫 Composition API 的程式碼，
// 所有定義的變數、方法都能直接在模板中使用。
import { ref } from 'vue'; // 引入 Vue 的 ref 方法，用於定義響應式變數
const num = ref(1);
function clickMe() {
    num.value++;
}
// 在 Vue 3.x 的 <script setup> 中不需要 return，
// return {
//     num,
//     clickMe
// };  
</script>
<template>
    <div>
        {{ num }}
        <!-- v-on 為監聽器，對他做特定動作可觸發特定函式 -->
        <button type="button" v-on:click="clickMe">點我加 1</button>
    </div>
</template>