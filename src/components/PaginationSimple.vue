<template>
  <div class="flex items-center gap-1">
    <div class="pagination-container" ref="container">
      <button
        v-for="page in [1, 2, 3, 4, 5]"
        :key="page"
        @click="currentPage = page"
        :class="[
          'pagination-btn',
          { 'active': currentPage === page }
        ]"
        :data-page="page"
      >
        {{ page }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick, onMounted } from 'vue';

const currentPage = ref(1);
const container = ref(null);

const updateSlider = async () => {
  await nextTick();
  
  if (!container.value) return;
  
  const activeBtn = container.value.querySelector('.pagination-btn.active');
  if (!activeBtn) return;
  
  const containerRect = container.value.getBoundingClientRect();
  const btnRect = activeBtn.getBoundingClientRect();
  
  const left = btnRect.left - containerRect.left;
  const width = btnRect.width;
  
  container.value.style.setProperty('--slider-left', `${left}px`);
  container.value.style.setProperty('--slider-width', `${width}px`);
};

onMounted(() => {
  updateSlider();
});

watch(currentPage, () => {
  updateSlider();
});
</script>

<style scoped>
.pagination-container {
  position: relative;
  display: flex;
  align-items: center;
  gap: 4px;
  background: #f1f5f9;
  padding: 4px;
  border-radius: 8px;
}

.pagination-container::before {
  content: '';
  position: absolute;
  top: 4px;
  left: var(--slider-left, 4px);
  width: var(--slider-width, 40px);
  height: calc(100% - 8px);
  background: #0f172a;
  border-radius: 6px;
  transition: all 300ms ease-in-out;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
  z-index: 1;
}

.pagination-btn {
  position: relative;
  z-index: 2;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  font-size: 14px;
  font-weight: 500;
  color: #64748b;
  background: transparent;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: all 200ms ease-in-out;
  white-space: nowrap;
  user-select: none;
}

.pagination-btn:hover {
  color: #475569;
}

.pagination-btn.active {
  color: white;
  font-weight: 600;
}

.pagination-btn:focus {
  outline: 2px solid #3b82f6;
  outline-offset: 2px;
}
</style> 