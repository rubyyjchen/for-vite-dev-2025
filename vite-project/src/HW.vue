<script setup>
import HWOne from './HWOne.vue';
import HWTwo from './HWTwo.vue';
import HWThree from './HWThree.vue';
import { ref } from 'vue';
const hwList = ref([
    { name: 'HWOne', component: HWOne },
    { name: 'HWTwo', component: HWTwo },
    { name: 'HWThree', component: HWThree }
]);
const currentHW = ref(hwList.value[0].component);
</script>
<template>
  <div>
    <button v-for="hw in hwList" :key="hw.name" @click="currentHW = hw.component">
      {{ hw.name }}
    </button>
    <component :is="currentHW" />
  </div>
</template>