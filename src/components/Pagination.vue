<template>
  <div 
    :class="paginationClass"
    :data-rounded="rounded"
    :data-compact="compact"
  >
    <!-- 上一页按钮 -->
    <button
      v-if="showArrows"
      :disabled="currentPage === 1"
      @click="goToPage(currentPage - 1)"
      :class="arrowButtonClass(false)"
      aria-label="上一页"
    >
      <ChevronLeft :size="16" />
    </button>

    <!-- 页码列表容器 -->
    <div 
      :class="pagesContainerClass" 
      ref="pagesContainer"
      :data-variant="variant"
      :data-rounded="rounded"
      :data-compact="compact"
    >
      <!-- 第一页 -->
      <button
        v-if="showFirstPage"
        ref="firstPageRef"
        @click="goToPage(1)"
        :class="[
          pageButtonClass, 
          { 
            'active': currentPage === 1 && showSlider
          }
        ]"
        :data-page="1"
      >
        1
      </button>

      <!-- 前省略号 -->
      <span v-if="showStartEllipsis" :class="ellipsisClass">...</span>

      <!-- 中间页码 -->
      <button
        v-for="page in visiblePages"
        :key="page"
        :ref="el => setPageRef(page, el)"
        @click="goToPage(page)"
        :class="[
          pageButtonClass, 
          { 
            'active': currentPage === page && showSlider
          }
        ]"
        :data-page="page"
      >
        {{ page }}
      </button>

      <!-- 后省略号 -->
      <span v-if="showEndEllipsis" :class="ellipsisClass">...</span>

      <!-- 最后一页 -->
      <button
        v-if="showLastPage"
        ref="lastPageRef"
        @click="goToPage(totalPages)"
        :class="[
          pageButtonClass, 
          { 
            'active': currentPage === totalPages && showSlider
          }
        ]"
        :data-page="totalPages"
      >
        {{ totalPages }}
      </button>
    </div>

    <!-- 下一页按钮 -->
    <button
      v-if="showArrows"
      :disabled="currentPage === totalPages"
      @click="goToPage(currentPage + 1)"
      :class="arrowButtonClass(true)"
      aria-label="下一页"
    >
      <ChevronRight :size="16" />
    </button>
  </div>
</template>

<script setup>
import { computed, ref, nextTick, onMounted, watch } from 'vue';
import { ChevronLeft, ChevronRight } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  currentPage: {
    type: Number,
    default: 1,
  },
  totalPages: {
    type: Number,
    required: true,
    validator: (value) => value > 0,
  },
  
  // 显示控制
  showArrows: {
    type: Boolean,
    default: true,
  },
  maxVisiblePages: {
    type: Number,
    default: 7,
    validator: (value) => value >= 3 && value % 2 === 1, // 必须是奇数且至少为3
  },
  
  // 样式
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'primary', 'minimal'].includes(value),
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  
  // 功能选项
  compact: {
    type: Boolean,
    default: false,
  },
  rounded: {
    type: Boolean,
    default: false,
  },
  
  // 禁用状态
  disabled: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:currentPage', 'change']);

// 模板引用
const pagesContainer = ref(null);
const pageRefs = ref(new Map());
const firstPageRef = ref(null);
const lastPageRef = ref(null);

// 移除sliderStyle，现在使用CSS变量

// 设置页码引用
const setPageRef = (page, el) => {
  if (el) {
    pageRefs.value.set(page, el);
  } else {
    pageRefs.value.delete(page);
  }
};

// 计算可见页码
const visiblePages = computed(() => {
  const { currentPage, totalPages, maxVisiblePages } = props;
  
  if (totalPages <= maxVisiblePages) {
    return Array.from({ length: totalPages }, (_, i) => i + 1);
  }

  const halfVisible = Math.floor(maxVisiblePages / 2);
  let start = currentPage - halfVisible;
  let end = currentPage + halfVisible;

  // 调整起始位置
  if (start < 1) {
    start = 1;
    end = maxVisiblePages;
  }
  
  if (end > totalPages) {
    end = totalPages;
    start = totalPages - maxVisiblePages + 1;
  }

  // 如果显示第一页，调整范围
  if (start <= 2) {
    start = 1;
    end = Math.min(maxVisiblePages, totalPages);
  }
  
  // 如果显示最后一页，调整范围
  if (end >= totalPages - 1) {
    end = totalPages;
    start = Math.max(1, totalPages - maxVisiblePages + 1);
  }

  return Array.from({ length: end - start + 1 }, (_, i) => start + i);
});

// 是否显示第一页
const showFirstPage = computed(() => {
  return props.totalPages > props.maxVisiblePages && !visiblePages.value.includes(1);
});

// 是否显示最后一页
const showLastPage = computed(() => {
  return props.totalPages > props.maxVisiblePages && !visiblePages.value.includes(props.totalPages);
});

// 是否显示开始省略号
const showStartEllipsis = computed(() => {
  return showFirstPage.value && visiblePages.value[0] > 2;
});

// 是否显示结束省略号
const showEndEllipsis = computed(() => {
  return showLastPage.value && visiblePages.value[visiblePages.value.length - 1] < props.totalPages - 1;
});

// 是否显示滑块
const showSlider = computed(() => {
  return !props.disabled;
});

// 样式计算
const paginationClass = computed(() => {
  const baseClasses = ['flex items-center'];
  
  if (props.compact) {
    baseClasses.push('gap-0');
    // 紧凑模式下添加整体背景
    if (!props.disabled) {
      baseClasses.push('bg-slate-100');
      if (props.rounded) {
        baseClasses.push('rounded-full');
      } else {
        baseClasses.push('rounded-lg');
      }
    }
  } else {
    baseClasses.push('gap-1');
  }
  
  if (props.disabled) {
    baseClasses.push('opacity-50 pointer-events-none');
  }
  
  return baseClasses;
});

const pagesContainerClass = computed(() => {
  const baseClasses = ['pagination-container relative flex items-center'];
  
  if (props.compact) {
    baseClasses.push('gap-0');
    // 紧凑模式下不需要独立背景容器，整体背景由父容器处理
  } else {
    baseClasses.push('gap-1');
    // 正常模式下不显示背景容器，但保留滑块功能
  }
  
  return baseClasses;
});

// 移除sliderClass，现在使用CSS伪元素

const pageButtonClass = computed(() => {
  const baseClasses = [
    'pagination-btn relative inline-flex items-center justify-center font-medium transition-all duration-200',
    'cursor-pointer text-slate-500 rounded-md whitespace-nowrap select-none hover:text-slate-600',
    'focus:outline-none',
  ];
  
  // 尺寸 - 确保按钮尺寸一致
  switch (props.size) {
    case 'sm':
      baseClasses.push('h-8 min-w-8 px-2 text-sm flex-shrink-0');
      break;
    case 'lg':
      baseClasses.push('h-12 min-w-12 px-4 text-base flex-shrink-0');
      break;
    default:
      baseClasses.push('h-10 min-w-10 px-3 text-sm flex-shrink-0');
  }
  
  // 圆角处理
  if (props.compact) {
    // 紧凑模式下按钮无圆角，由容器统一处理
    baseClasses.push('rounded-none');
  } else {
    // 非紧凑模式下每个按钮独立圆角
    baseClasses.push(props.rounded ? 'rounded-full' : 'rounded-lg');
  }
  
  // 每个按钮都有独立样式
  if (props.compact) {
    // 紧凑模式下不需要独立背景
    baseClasses.push('hover:bg-slate-50/50');
  } else {
    // 正常模式下每个按钮都有背景
    switch (props.variant) {
      case 'primary':
        baseClasses.push('bg-white border border-slate-200 hover:bg-blue-50 hover:border-blue-200');
        break;
      case 'minimal':
        baseClasses.push('bg-white hover:bg-slate-100');
        break;
      default:
        baseClasses.push('bg-white border border-slate-200 hover:bg-slate-50 hover:border-slate-300');
    }
  }
  
  return baseClasses;
});

const arrowButtonClass = computed(() => (isNext) => {
  const baseClasses = [
    'inline-flex items-center justify-center font-medium transition-all duration-200',
    'focus:outline-none',
  ];
  
  // 尺寸 - 确保宽高固定，不会因为内容变化而变形
  switch (props.size) {
    case 'sm':
      baseClasses.push('h-8 w-8 min-w-8 text-sm flex-shrink-0');
      break;
    case 'lg':
      baseClasses.push('h-12 w-12 min-w-12 text-base flex-shrink-0');
      break;
    default:
      baseClasses.push('h-10 w-10 min-w-10 text-sm flex-shrink-0');
  }
  
  // 圆角处理
  if (props.compact) {
    // 紧凑模式下箭头按钮没有独立圆角
    baseClasses.push('rounded-none');
  } else {
    baseClasses.push(props.rounded ? 'rounded-full' : 'rounded-lg');
  }
  
  // 禁用状态
  const isDisabled = (isNext && props.currentPage === props.totalPages) || 
                    (!isNext && props.currentPage === 1);
  
  if (isDisabled) {
    baseClasses.push('bg-slate-100 text-slate-400 cursor-not-allowed');
  } else {
    if (props.compact) {
      // 紧凑模式下箭头按钮透明背景
      baseClasses.push('text-slate-600 hover:text-slate-900 bg-transparent');
    } else {
      // 正常模式下箭头按钮有背景
      switch (props.variant) {
        case 'primary':
          baseClasses.push('bg-white text-slate-600 border border-slate-200');
          baseClasses.push('hover:bg-blue-50 hover:border-blue-200 hover:text-blue-700');
          break;
        case 'minimal':
          baseClasses.push('text-slate-600 hover:text-slate-900 hover:bg-slate-100');
          break;
        default:
          baseClasses.push('bg-white text-slate-600 border border-slate-200');
          baseClasses.push('hover:bg-slate-50 hover:border-slate-300 hover:text-slate-700');
      }
    }
  }
  
  return baseClasses;
});

const ellipsisClass = computed(() => {
  const baseClasses = ['inline-flex items-center justify-center text-slate-400 flex-shrink-0'];
  
  // 在正常模式下给省略号也加背景，保持一致性
  if (!props.compact) {
    baseClasses.push('bg-white border border-slate-200');
    if (props.rounded) {
      baseClasses.push('rounded-full');
    } else {
      baseClasses.push('rounded-lg');
    }
  }
  
  switch (props.size) {
    case 'sm':
      baseClasses.push('h-8 min-w-8 px-2 text-sm');
      break;
    case 'lg':
      baseClasses.push('h-12 min-w-12 px-4 text-base');
      break;
    default:
      baseClasses.push('h-10 min-w-10 px-3 text-sm');
  }
  
  return baseClasses;
});

// 移除不再使用的辅助函数

// 更新滑块位置
const updateSliderPosition = async (retryCount = 0) => {
  if (!showSlider.value || !pagesContainer.value) return;
  
  await nextTick();
  
  let targetElement = null;
  
  // 查找当前页码对应的按钮元素
  if (showFirstPage.value && props.currentPage === 1) {
    targetElement = firstPageRef.value;
  } else if (showLastPage.value && props.currentPage === props.totalPages) {
    targetElement = lastPageRef.value;
  } else {
    targetElement = pageRefs.value.get(props.currentPage);
  }
  
  // 如果通过引用找不到，尝试通过DOM查询找到
  if (!targetElement && pagesContainer.value) {
    targetElement = pagesContainer.value.querySelector(`[data-page="${props.currentPage}"]`);
  }
  
  if (!targetElement) {
    // 如果找不到目标元素，最多重试3次
    if (retryCount < 3) {
      await nextTick();
      return updateSliderPosition(retryCount + 1);
    } else {
      // 重试3次后仍然找不到元素，放弃更新
      console.warn('无法找到目标页码元素，跳过滑块位置更新');
      return;
    }
  }
  
  const containerRect = pagesContainer.value.getBoundingClientRect();
  const targetRect = targetElement.getBoundingClientRect();
  
  const left = targetRect.left - containerRect.left;
  const width = targetRect.width;
  const height = targetRect.height;
  
  // 使用CSS变量设置滑块位置
  let adjustedLeft = left;
  let adjustedWidth = width;
  let adjustedHeight = height;
  let containerPadding = 0;
  
  if (props.compact) {
    // 紧凑模式下，滑块需要完全贴合按钮
    // 确保滑块高度和容器高度一致
    const containerHeight = pagesContainer.value.offsetHeight;
    adjustedHeight = containerHeight;
    containerPadding = 0;
  } else {
    // 正常模式下的计算保持不变
    containerPadding = 0;
  }
  
  pagesContainer.value.style.setProperty('--slider-left', `${adjustedLeft}px`);
  pagesContainer.value.style.setProperty('--slider-width', `${adjustedWidth}px`);
  pagesContainer.value.style.setProperty('--slider-height', `${adjustedHeight}px`);
  pagesContainer.value.style.setProperty('--container-padding', `${containerPadding}px`);
};

// 事件处理
const goToPage = (page) => {
  if (props.disabled || page === props.currentPage || page < 1 || page > props.totalPages) {
    return;
  }
  
  emit('update:currentPage', page);
  emit('change', page);
};

// 监听器和生命周期
onMounted(async () => {
  // 等待DOM完全渲染后再更新滑块位置
  await nextTick();
  await nextTick(); // 双重等待确保所有元素都已渲染
  updateSliderPosition();
});

watch(() => props.currentPage, async () => {
  // 页码变化时立即更新滑块位置
  await nextTick();
  updateSliderPosition();
}, { immediate: false });

watch(visiblePages, async () => {
  // 可见页码变化时更新滑块位置
  await nextTick();
  updateSliderPosition();
}, { flush: 'post' });

watch([() => props.variant, () => props.size, () => props.compact, () => props.rounded], async () => {
  // 样式属性变化时更新滑块位置
  await nextTick();
  updateSliderPosition();
}, { flush: 'post' });
</script>

<style scoped>
/* 分页容器和滑块样式 */
.pagination-container::before {
  content: '';
  position: absolute;
  left: var(--slider-left, 0px);
  top: var(--container-padding, 0px);
  width: var(--slider-width, 40px);
  height: var(--slider-height, 40px);
  background: #0f172a;
  border-radius: 6px;
  transition: left 250ms cubic-bezier(0.25, 0.46, 0.45, 0.94), width 250ms cubic-bezier(0.25, 0.46, 0.45, 0.94);
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1);
  z-index: 3;
  opacity: 1;
}

/* 紧凑模式下滑块完全贴合 */
.pagination-container[data-compact="true"]::before {
  top: 0;
  left: var(--slider-left, 0px);
  width: var(--slider-width, 40px);
  height: 100%;
  border-radius: 0;
}

/* 紧凑模式下滑块的圆角处理 */
.pagination-container[data-compact="true"][data-rounded="true"]::before {
  border-radius: 6px;
}

.pagination-container[data-compact="true"][data-rounded="false"]::before {
  border-radius: 4px;
}

/* 确保紧凑模式下滑块在页码按钮上方 */
.pagination-container[data-compact="true"] .pagination-btn {
  position: relative;
  z-index: 1;
}

/* 滑块始终显示，通过背景层实现 */

.pagination-btn {
  position: relative;
  z-index: 1;
  background: transparent;
  border: none;
}

/* 激活状态的按钮样式 */
.pagination-btn.active {
  color: white !important;
  font-weight: 600 !important;
  z-index: 4 !important;
}

.pagination-btn.active:hover {
  color: white !important;
}

/* 正常模式下激活按钮不显示自己的背景，让滑块显示 */
.pagination-container:not([data-compact="true"]) .pagination-btn.active {
  background: transparent !important;
  border-color: transparent !important;
}

/* 确保所有页码按钮都有背景色 */
.pagination-container:not([data-compact="true"]) .pagination-btn {
  background: white !important;
  border: 1px solid #e2e8f0 !important;
}

.pagination-container:not([data-compact="true"]) .pagination-btn:hover:not(.active) {
  background: #f8fafc !important;
  border-color: #cbd5e1 !important;
}

/* 圆形按钮样式 - 确保在非紧凑模式下按钮也是圆形 */
.pagination-container[data-rounded="true"]:not([data-compact="true"]) .pagination-btn {
  border-radius: 9999px !important;
}

.pagination-container[data-rounded="false"]:not([data-compact="true"]) .pagination-btn {
  border-radius: 6px !important;
}



/* 变体样式 */
.pagination-container[data-variant="primary"]::before {
  background: #2563eb;
}

.pagination-container[data-variant="minimal"]::before {
  background: #0f172a;
}

.pagination-container[data-variant="default"]::before {
  background: #0f172a;
}

/* 圆角样式 */
.pagination-container[data-rounded="true"]:not([data-compact="true"])::before {
  border-radius: 9999px;
}

.pagination-container[data-rounded="false"]:not([data-compact="true"])::before {
  border-radius: 6px;
}

/* 紧凑模式下的圆角处理 */
.pagination-container[data-compact="true"][data-rounded="true"]::before {
  border-radius: 9999px;
}

.pagination-container[data-compact="true"][data-rounded="false"]::before {
  border-radius: 6px;
}

/* 紧凑模式下的按钮样式 */
.pagination-container[data-compact="true"] .pagination-btn {
  border-radius: 0;
}

.pagination-container[data-compact="true"] .pagination-btn:first-of-type {
  border-top-left-radius: 6px;
  border-bottom-left-radius: 6px;
}

.pagination-container[data-compact="true"] .pagination-btn:last-of-type {
  border-top-right-radius: 6px;
  border-bottom-right-radius: 6px;
}

/* 紧凑模式下的整体圆角处理 */
.bg-slate-100.rounded-lg {
  padding: 0;
}

/* 紧凑模式下第一个和最后一个元素的圆角 - 包括箭头 */
.rounded-lg > *:first-child {
  border-top-left-radius: 6px !important;
  border-bottom-left-radius: 6px !important;
}

.rounded-lg > *:last-child {
  border-top-right-radius: 6px !important;
  border-bottom-right-radius: 6px !important;
}

.rounded-full > *:first-child {
  border-top-left-radius: 9999px !important;
  border-bottom-left-radius: 9999px !important;
}

.rounded-full > *:last-child {
  border-top-right-radius: 9999px !important;
  border-bottom-right-radius: 9999px !important;
}

.pagination-container[data-compact="true"] .pagination-btn {
  outline: none;
}

/* 箭头按钮的圆形样式 - 确保在圆形模式下箭头按钮也是圆形 */
.pagination-container[data-rounded="true"] + button,
.pagination-container[data-rounded="true"] ~ button {
  border-radius: 9999px !important;
}

/* 为了确保所有按钮在圆形模式下都是圆形，包括箭头按钮 */
.rounded-full .pagination-btn,
.rounded-full button {
  border-radius: 9999px !important;
}

/* 省略号的圆形样式 */
.pagination-container[data-rounded="true"]:not([data-compact="true"]) span {
  border-radius: 9999px !important;
}

/* 确保所有 UnoCSS 的 rounded-full 类都能正确生效 */
.rounded-full {
  border-radius: 9999px !important;
}
</style>

 