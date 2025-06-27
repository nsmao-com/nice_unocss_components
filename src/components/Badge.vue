<template>
  <span :class="badgeClasses" v-if="shouldShow">
    <slot>{{ displayContent }}</slot>
  </span>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  // 徽章内容
  content: {
    type: [String, Number],
    default: '',
  },
  // 徽章类型
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'success', 'warning', 'danger', 'info'].includes(value),
  },
  // 徽章大小
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  // 是否显示为点状
  dot: {
    type: Boolean,
    default: false,
  },
  // 最大数字，超过显示 99+
  max: {
    type: Number,
    default: 99,
  },
  // 是否显示0
  showZero: {
    type: Boolean,
    default: false,
  },
  // 自定义颜色
  color: {
    type: String,
    default: '',
  },
  // 是否为方形
  square: {
    type: Boolean,
    default: false,
  },
  // 是否为轮廓样式
  outline: {
    type: Boolean,
    default: false,
  },
});

// 是否应该显示徽章
const shouldShow = computed(() => {
  if (props.dot) return true;
  if (props.content === 0 || props.content === '0') {
    return props.showZero;
  }
  return props.content !== '' && props.content !== null && props.content !== undefined;
});

// 显示的内容
const displayContent = computed(() => {
  if (props.dot) return '';
  if (typeof props.content === 'number' && props.content > props.max) {
    return `${props.max}+`;
  }
  return props.content;
});

// 基础样式
const baseClasses = computed(() => {
  const classes = [
    'inline-flex items-center justify-center font-bold text-xs leading-none',
    'transition-all duration-200',
    'shadow-sm', // 添加轻微阴影
  ];

  // 大小
  if (props.dot) {
    switch (props.size) {
      case 'sm':
        classes.push('w-2.5 h-2.5');
        break;
      case 'md':
        classes.push('w-3 h-3');
        break;
      case 'lg':
        classes.push('w-3.5 h-3.5');
        break;
    }
    classes.push('border-2 border-white'); // 状态点添加白色边框
  } else {
    switch (props.size) {
      case 'sm':
        classes.push('min-w-5 h-5 px-1.5 text-xs');
        break;
      case 'md':
        classes.push('min-w-6 h-6 px-2 text-xs');
        break;
      case 'lg':
        classes.push('min-w-7 h-7 px-2.5 text-sm');
        break;
    }
  }

  // 形状
  if (props.square) {
    classes.push('rounded-md'); // 方形徽章更圆润
  } else {
    classes.push('rounded-full');
  }

  return classes;
});

// 颜色样式
const colorClasses = computed(() => {
  if (props.color) {
    return props.outline 
      ? `border-2 text-[${props.color}] border-[${props.color}] bg-transparent`
      : `bg-[${props.color}] text-white`;
  }

  const variants = {
    primary: props.outline 
      ? 'border-2 border-blue-500 text-blue-500 bg-transparent'
      : 'bg-blue-500 text-white',
    secondary: props.outline
      ? 'border-2 border-slate-500 text-slate-500 bg-transparent'
      : 'bg-slate-500 text-white',
    success: props.outline
      ? 'border-2 border-green-500 text-green-500 bg-transparent'
      : 'bg-green-500 text-white',
    warning: props.outline
      ? 'border-2 border-amber-500 text-amber-500 bg-transparent'
      : 'bg-amber-500 text-white',
    danger: props.outline
      ? 'border-2 border-red-500 text-red-500 bg-transparent'
      : 'bg-red-500 text-white',
    info: props.outline
      ? 'border-2 border-cyan-500 text-cyan-500 bg-transparent'
      : 'bg-cyan-500 text-white',
  };

  return variants[props.variant] || variants.primary;
});

// 最终样式类
const badgeClasses = computed(() => [
  ...baseClasses.value,
  colorClasses.value,
]);
</script> 