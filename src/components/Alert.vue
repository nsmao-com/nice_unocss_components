<template>
  <div 
    role="alert" 
    :data-visible="visible" 
    :data-has-title="!!title" 
    :title="title" 
    :class="alertClass"
    v-if="visible"
  >
    <!-- 图标容器 -->
    <div v-if="showIcon" :class="iconContainerClass">
      <svg 
        :class="iconClass"
        viewBox="0 0 24 24" 
        fill="none" 
        xmlns="http://www.w3.org/2000/svg"
      >
        <g v-html="currentIconSVG"></g>
      </svg>
    </div>
    
    <!-- 内容区域 -->
    <div :class="contentClass">
      <div :class="messageClass">
        <slot>{{ message || title }}</slot>
      </div>
    </div>
    
    <!-- 关闭按钮 -->
    <div v-if="closable" class="ml-3">
      <button
        @click="handleClose"
        :class="closeButtonClass"
      >
        <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M18 6L6 18M6 6l12 12" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  // 基础属性
  title: { type: String, default: '' },
  message: { type: String, default: '' },
  variant: { type: String, default: 'default' }, // default, primary, secondary, success, warning, danger
  
  // 显示控制
  visible: { type: Boolean, default: true },
  closable: { type: Boolean, default: false },
  
  // 图标
  icon: { type: String, default: null }, // 自定义SVG路径
  showIcon: { type: Boolean, default: true },
  iconSize: { type: Number, default: 20 },
  
  // 样式
  size: { type: String, default: 'md' }, // sm, md, lg
  rounded: { type: Boolean, default: false },
});

const emit = defineEmits(['close']);

// 当前显示状态
const visible = ref(props.visible);

// 默认SVG图标路径
const defaultIconSVGs = {
  default: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M12 16v-4M12 8h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>',
  primary: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M12 16v-4M12 8h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>',
  secondary: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3M12 17h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>',
  success: '<path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><path d="m9 11 3 3L22 4" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
  warning: '<path d="m21.73 18-8-14a2 2 0 0 0-3.48 0l-8 14A2 2 0 0 0 4 21h16a2 2 0 0 0 1.73-3Z" stroke="currentColor" stroke-width="2" fill="none" stroke-linejoin="round"/><path d="M12 9v4M12 17h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>',
  danger: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M15 9l-6 6M9 9l6 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>',
};

// 当前图标SVG
const currentIconSVG = computed(() => {
  if (!props.showIcon) return '';
  return props.icon || defaultIconSVGs[props.variant] || defaultIconSVGs.default;
});

// Alert容器样式
const alertClass = computed(() => {
  const baseClasses = [
    'flex flex-grow flex-row w-full py-3 px-4 gap-x-1 rounded-lg items-start',
  ];

  // 变体颜色 - 稍微深一点的背景色和文字色
  switch (props.variant) {
    case 'default':
      baseClasses.push('bg-gray-100 text-gray-700');
      break;
    case 'primary':
      baseClasses.push('bg-blue-100 text-blue-700');
      break;
    case 'secondary':
      baseClasses.push('bg-purple-100 text-purple-700');
      break;
    case 'success':
      baseClasses.push('bg-green-100 text-green-700');
      break;
    case 'warning':
      baseClasses.push('bg-yellow-100 text-yellow-700');
      break;
    case 'danger':
      baseClasses.push('bg-red-100 text-red-700');
      break;
  }

  return baseClasses;
});

// 图标容器样式
const iconContainerClass = computed(() => {
  const baseClasses = [
    'flex-none relative w-9 h-9 rounded-full grid place-items-center border shadow-sm border-1'
  ];

  // 图标容器颜色 - 稍微深一点的背景色和边框色
  switch (props.variant) {
    case 'default':
      baseClasses.push('bg-gray-50 border-gray-200');
      break;
    case 'primary':
      baseClasses.push('bg-blue-50 border-blue-200');
      break;
    case 'secondary':
      baseClasses.push('bg-purple-50 border-purple-200');
      break;
    case 'success':
      baseClasses.push('bg-white border-green-150');
      break;
    case 'warning':
      baseClasses.push('bg-white border-yellow-150');
      break;
    case 'danger':
      baseClasses.push('bg-white border-red-150');
      break;
  }

  return baseClasses;
});

// 图标样式
const iconClass = computed(() => {
  const baseClasses = [
    'w-6 h-6'
  ];

  // 图标颜色 - 稍微深一点的图标色
  switch (props.variant) {
    case 'default':
      baseClasses.push('text-gray-600');
      break;
    case 'primary':
      baseClasses.push('text-blue-600');
      break;
    case 'secondary':
      baseClasses.push('text-purple-600');
      break;
    case 'success':
      baseClasses.push('text-green-500');
      break;
    case 'warning':
      baseClasses.push('text-yellow-500');
      break;
    case 'danger':
      baseClasses.push('text-red-500');
      break;
  }

  return baseClasses;
});

// 内容区域样式
const contentClass = computed(() => [
  'h-full flex-grow min-h-10 ms-2 flex flex-col box-border text-inherit justify-center items-center'
]);

// 消息文本样式
const messageClass = computed(() => [
  'text-sm w-full font-medium block text-inherit leading-5'
]);

// 关闭按钮样式
const closeButtonClass = computed(() => {
  const baseClasses = [
    'flex-shrink-0 p-1 rounded transition-colors duration-200',
    'hover:bg-black/5 focus:outline-none text-inherit opacity-70 hover:opacity-100'
  ];

  return baseClasses;
});

// 处理关闭
const handleClose = () => {
  visible.value = false;
  emit('close');
};
</script> 