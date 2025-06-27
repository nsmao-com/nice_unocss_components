<template>
  <div class="flex items-center gap-1">
    <div class="relative flex items-center gap-1 bg-slate-100 rounded-lg p-1" ref="container">
      <!-- 滑块背景 -->
      <div 
        class="absolute bg-slate-900 rounded-lg transition-all duration-300 z-1 shadow-sm"
        :style="sliderStyle"
      ></div>
      
      <!-- 页码按钮 -->
      <button
        v-for="page in [1, 2, 3, 4, 5]"
        :key="page"
        :ref="el => setPageRef(page, el)"
        @click="currentPage = page"
        :class="[
          'relative h-10 min-w-10 px-3 text-sm inline-flex items-center justify-center font-medium transition-all duration-200 z-2',
          'cursor-pointer rounded-lg whitespace-nowrap select-none',
          'focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-1',
          {
            'text-white font-semibold': currentPage === page,
            'text-slate-500 hover:text-slate-600': currentPage !== page
          }
        ]"
      >
        {{ page }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick, watch, onMounted } from 'vue';

const currentPage = ref(1);
const container = ref(null);
const pageRefs = ref(new Map());
const sliderStyle = ref({});

const setPageRef = (page, el) => {
  if (el) {
    pageRefs.value.set(page, el);
  } else {
    pageRefs.value.delete(page);
  }
};

const updateSlider = async () => {
  await nextTick();
  
  const targetElement = pageRefs.value.get(currentPage.value);
  if (!targetElement) return;
  
  const width = targetElement.offsetWidth;
  const height = targetElement.offsetHeight;
  const left = targetElement.offsetLeft;
  
  sliderStyle.value = {
    width: `${width}px`,
    height: `${height}px`,
    transform: `translateX(${left}px)`,
    top: '0px',
    left: '0px',
  };
};

onMounted(() => {
  updateSlider();
});

watch(currentPage, () => {
  updateSlider();
});
</script>

<style scoped>
.z-1 { z-index: 1; }
.z-2 { z-index: 2; }
</style> 