<template>
  <div class="container">
    <base-checkbox
      v-model="disabled"
      label="停用主題切換"
      class="border rounded p-4"
    />

    <div class="toggle-wrapper">
      <toggle-proactive
        v-model="isDarkMode"
        :disabled="disabled"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watch, onMounted } from 'vue'
import BaseCheckbox from '../../base-checkbox.vue'
import ToggleProactive from '../toggle-proactive.vue'

const disabled = ref(false)
const isDarkMode = ref(false)

// 加载主题状态
onMounted(() => {
  const theme = localStorage.getItem('theme')
  if (theme === 'dark') {
    isDarkMode.value = true
    document.body.classList.add('dark-mode')
  }
})

// 切换主题状态
watch(isDarkMode, (newVal) => {
  if (newVal) {
    document.body.classList.add('dark-mode')
    localStorage.setItem('theme', 'dark')
  } else {
    document.body.classList.remove('dark-mode')
    localStorage.setItem('theme', 'light')
  }
})
</script>

<style scoped>
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  border: 1px solid #ccc;
  padding: 1.5rem;
}

.toggle-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 开关样式 */
.switch {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 24px;
}
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}
.slider {
  position: absolute;
  cursor: pointer;
  top: 0; left: 0; right: 0; bottom: 0;
  background-color: #ccc;
  border-radius: 24px;
  transition: 0.4s;
}
.slider:before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  left: 3px;
  bottom: 3px;
  background-color: white;
  border-radius: 50%;
  transition: 0.4s;
}
input:checked + .slider {
  background-color: #2196F3;
}
input:checked + .slider:before {
  transform: translateX(26px);
}

/* 暗黑模式样式 */
body.dark-mode {
  background-color: #1a1a1a;
  color: #f1f1f1;
}
body.dark-mode header,
body.dark-mode footer {
  background-color: #222;
}
body.dark-mode .hero {
  background: linear-gradient(135deg, #672b9a, #333);
}
body.dark-mode .news-card,
body.dark-mode .news-card1 {
  background-color: #2a2a2a;
}
body.dark-mode .card-header,
body.dark-mode .card-header1 {
  background-color: #333;
}
body.dark-mode .sdg-tag,
body.dark-mode .sdg-tag1 {
  background-color: #8833cc;
}
body.dark-mode .cta-button {
  background-color: #ff8566;
  color: #fff;
}
body.dark-mode .map-section {
  background-color: #1e1e1e;
}
</style>
