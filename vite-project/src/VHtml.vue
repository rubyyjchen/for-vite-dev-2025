<script setup>
import { ref } from 'vue'
const htmlTemplate = ref('<h1>這是HTML片段</h1>')
</script>
<template>
    <div>
        {{ htmlTemplate }}
        <div v-text="htmlTemplate"></div>
        <div v-html="htmlTemplate"></div>
    </div>
</template>