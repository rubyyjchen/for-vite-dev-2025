
<script setup>
import { ref } from 'vue'
import App from './App.vue'
import AppNew from './AppNew.vue'
import VModel from './VModel.vue'
import HWOne from './HWOne.vue'
import HWTwo from './HWTwo.vue'
import HWThree from './HWThree.vue'

const currentPage = ref('hw1')
const activeDropdown = ref(null)

const toggleDropdown = (dropdown) => {
  if (activeDropdown.value === dropdown) {
    activeDropdown.value = null
  } else {
    activeDropdown.value = dropdown
  }
}

const selectPage = (page) => {
  currentPage.value = page
  activeDropdown.value = null
}

// 點擊外部關閉下拉選單
const closeDropdowns = () => {
  activeDropdown.value = null
}

// 監聽點擊事件
document.addEventListener('click', (e) => {
  if (!e.target.closest('.dropdown')) {
    closeDropdowns()
  }
})
</script>

<template>
  <div id="app">
    <!-- 導航欄直接寫在這裡 -->
    <nav class="navbar">
      <div class="nav-container">
        <!-- 標題 -->
        <div class="nav-title">
          <h2>Vue3 專案</h2>
        </div>
        
        <!-- 導航選單 -->
        <div class="nav-menu">
          <!-- Vue 下拉選單 -->
          <div class="dropdown">
            <button @click="toggleDropdown('vue')" class="dropdown-button">
              Vue
              <span class="dropdown-arrow">▼</span>
            </button>
            <div class="dropdown-menu" :class="{ 'show': activeDropdown === 'vue' }">
              <a @click="selectPage('init')" class="dropdown-item">Init</a>
              <a @click="selectPage('video')" class="dropdown-item">Video</a>
              <a @click="selectPage('v-model')" class="dropdown-item">V-Model</a>
            </div>
          </div>
          
          <!-- HW 下拉選單 -->
          <div class="dropdown">
            <button @click="toggleDropdown('hw')" class="dropdown-button">
              HW
              <span class="dropdown-arrow">▼</span>
            </button>
            <div class="dropdown-menu" :class="{ 'show': activeDropdown === 'hw' }">
              <a @click="selectPage('hw1')" class="dropdown-item">HW1</a>
              <a @click="selectPage('hw2')" class="dropdown-item">HW2</a>
              <a @click="selectPage('hw3')" class="dropdown-item">HW3</a>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <main class="main-content">
      <!-- 條件渲染不同的組件 -->
      <App v-if="currentPage === 'init'" />
      <AppNew v-else-if="currentPage === 'video'" />
      <VModel v-else-if="currentPage === 'v-model'" />
      <HWOne v-else-if="currentPage === 'hw1'" />
      <HWTwo v-else-if="currentPage === 'hw2'" />
      <HWThree v-else-if="currentPage === 'hw3'" />
      <HWOne v-else />
    </main>
  </div>
</template>

<style>
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  padding: 2rem;
  width: 1200px;
  margin: 0 auto;
}

/* 全域樣式 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
  background-color: #f8f9fa;
}

/* 導航欄樣式 */
.navbar {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 1rem 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.nav-container {
  width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-title h2 {
  color: white;
  margin: 0;
  font-size: 1.5rem;
  font-weight: 600;
}

.nav-menu {
  display: flex;
  gap: 1rem;
}

/* 下拉選單樣式 */
.dropdown {
  position: relative;
}

.dropdown-button {
  background: rgba(255, 255, 255, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.3s ease;
}

.dropdown-button:hover {
  background: rgba(255, 255, 255, 0.3);
}

.dropdown-arrow {
  font-size: 0.8rem;
  transition: transform 0.3s ease;
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  border: 1px solid #ddd;
  border-radius: 6px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
  min-width: 150px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-10px);
  transition: all 0.3s ease;
  z-index: 1000;
}

.dropdown-menu.show {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.dropdown-item {
  display: block;
  padding: 0.75rem 1rem;
  color: #333;
  text-decoration: none;
  transition: background-color 0.3s ease;
  cursor: pointer;
}

.dropdown-item:hover {
  background-color: #f8f9fa;
  color: #667eea;
}

@media (max-width: 768px) {
  .nav-container {
    flex-direction: column;
    gap: 1rem;
  }
  
  .nav-menu {
    flex-direction: column;
    gap: 1rem;
  }
}
</style> 