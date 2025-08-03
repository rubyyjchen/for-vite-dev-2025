<script setup>
import { ref } from 'vue'
const text = ref('這是一段文字')
const city = ref('請選擇城市')
const isChecked = ref(false)
const arrayCheckbox = ref([])
const radioValue = ref('男')
</script>
<template>
  <div>
    {{ text }}
    <input v-model="text" />
    <hr>
    <!-- 表單 -->
    {{ city }}
    <select name="" id="" v-model="city">
        <option value="Taipei">台北市</option>
        <option value="Taoyuan">桃園市</option>
        <option value="Hsinchu">新竹市</option>
    </select>
    <hr>
    <!-- checkbox 1. true or false 2. array value -->
    {{ isChecked }}
    <input type="checkbox" v-model="isChecked">
    <hr>
    {{ arrayCheckbox }}
    <input type="checkbox" value="type1" v-model="arrayCheckbox">type1
    <input type="checkbox" value="type2" v-model="arrayCheckbox">type2
    <input type="checkbox" value="type3" v-model="arrayCheckbox">type3
    <hr>
    <!-- radio -->
    {{ radioValue }}
    <input type="radio" value="男" v-model="radioValue">男
    <input type="radio" value="女" v-model="radioValue">女
    <hr>
  </div>
</template>