<template>
  <button
    ref="buttonRef"
    :class="[buttonClass, 'ripple-button']"
    @click="handleClick"
    @mousedown="handleMouseDown"
    :disabled="disabled"
  >
    <!-- 涟漪容器 -->
    <span class="absolute inset-0 overflow-hidden rounded-inherit">
      <span
        v-for="ripple in ripples"
        :key="ripple.id"
        class="absolute rounded-full bg-white/30 pointer-events-none animate-ripple"
        :style="{
          left: ripple.x + 'px',
          top: ripple.y + 'px',
          width: ripple.size + 'px',
          height: ripple.size + 'px',
          transform: 'translate(-50%, -50%)',
        }"
      ></span>
    </span>

    <!-- 按钮内容 -->
    <span class="relative z-10 flex items-center justify-center space-x-2">
      <!-- 图标插槽，优先级最高 -->
      <span v-if="$slots.icon" class="flex items-center">
        <slot name="icon"></slot>
      </span>
      <!-- 或者使用icon属性 -->
      <component v-else-if="icon" :is="icon" :size="iconSize" />
      
      <!-- 内容插槽，优先级高于text属性 -->
      <span v-if="$slots.default"><slot></slot></span>
      <span v-else-if="text">{{ text }}</span>
    </span>
  </button>
</template>

<script setup>
import { ref, computed, useSlots } from 'vue';

const props = defineProps({
  // 按钮文字
  text: {
    type: String,
    default: '',
  },
  // 按钮图标
  icon: {
    type: [String, Object, Function],
    default: null,
  },
  // 图标大小
  iconSize: {
    type: Number,
    default: 16,
  },
  // 按钮变体
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'outline', 'ghost', 'danger', 'success', 'warning'].includes(value),
  },
  // 按钮尺寸
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg', 'xl'].includes(value),
  },
  // 是否禁用
  disabled: {
    type: Boolean,
    default: false,
  },
  // 是否为圆形按钮
  rounded: {
    type: Boolean,
    default: false,
  },
  // 是否为全宽按钮
  fullWidth: {
    type: Boolean,
    default: false,
  },
  // 自定义类名
  customClass: {
    type: String,
    default: '',
  },
});

const emit = defineEmits(['click']);
const slots = useSlots();

const buttonRef = ref(null);
const ripples = ref([]);

// 判断是否为纯图标按钮
const isIconOnly = computed(() => {
  const hasDefaultSlot = !!slots.default;
  const hasIconSlot = !!slots.icon;
  return !props.text && !hasDefaultSlot && (props.icon || hasIconSlot);
});

// 按钮样式计算
const buttonClass = computed(() => {
  const baseClasses = [
    'relative inline-flex items-center justify-center font-medium transition-all duration-200 overflow-hidden',
    'focus:outline-none focus-visible:outline-none',
    'active:scale-95',
    'outline-none', // 去掉原生outline
  ];

  // 尺寸样式
  const sizeClasses = {
    sm: isIconOnly.value ? 'w-8 h-8 text-sm' : 'px-3 py-1.5 text-sm',
    md: isIconOnly.value ? 'w-10 h-10 text-sm' : 'px-4 py-2 text-sm',
    lg: isIconOnly.value ? 'w-12 h-12 text-base' : 'px-6 py-3 text-base',
    xl: isIconOnly.value ? 'w-16 h-16 text-lg' : 'px-8 py-4 text-lg',
  };

  // 变体样式
  const variantClasses = {
    primary: [
      'bg-blue-600 text-white border border-blue-600',
      'hover:bg-blue-700 hover:border-blue-700',
      'disabled:bg-blue-300 disabled:border-blue-300',
    ],
    secondary: [
      'bg-slate-600 text-white border border-slate-600',
      'hover:bg-slate-700 hover:border-slate-700',
      'disabled:bg-slate-300 disabled:border-slate-300',
    ],
    outline: [
      'bg-transparent text-blue-600 border border-blue-600',
      'hover:bg-blue-50 hover:text-blue-700',
      'disabled:text-blue-300 disabled:border-blue-300',
    ],
    ghost: [
      'bg-transparent text-slate-700 border border-transparent',
      'hover:bg-slate-100 hover:text-slate-900',
      'disabled:text-slate-300',
    ],
    danger: [
      'bg-red-600 text-white border border-red-600',
      'hover:bg-red-700 hover:border-red-700',
      'disabled:bg-red-300 disabled:border-red-300',
    ],
    success: [
      'bg-green-600 text-white border border-green-600',
      'hover:bg-green-700 hover:border-green-700',
      'disabled:bg-green-300 disabled:border-green-300',
    ],
    warning: [
      'bg-yellow-600 text-white border border-yellow-600',
      'hover:bg-yellow-700 hover:border-yellow-700',
      'disabled:bg-yellow-300 disabled:border-yellow-300',
    ],
  };

  // 圆角样式 - 纯图标按钮自动为圆形
  const roundedClasses = (props.rounded || isIconOnly.value) ? 'rounded-full' : 'rounded-lg';

  // 宽度样式
  const widthClasses = props.fullWidth ? 'w-full' : '';

  // 禁用状态
  const disabledClasses = props.disabled ? 'cursor-not-allowed opacity-60' : 'cursor-pointer';

  return [
    ...baseClasses,
    sizeClasses[props.size] || sizeClasses.md,
    ...(variantClasses[props.variant] || variantClasses.primary),
    roundedClasses,
    widthClasses,
    disabledClasses,
    props.customClass,
  ].filter(Boolean).join(' ');
});

// 处理点击事件
const handleClick = (event) => {
  if (props.disabled) return;
  emit('click', event);
};

// 处理鼠标按下事件，创建涟漪效果
const handleMouseDown = (event) => {
  if (props.disabled) return;
  
  const button = buttonRef.value;
  const rect = button.getBoundingClientRect();
  
  // 计算点击位置相对于按钮的坐标
  const x = event.clientX - rect.left;
  const y = event.clientY - rect.top;
  
  // 计算涟漪的最大尺寸（确保能覆盖整个按钮）
  const size = Math.max(
    Math.sqrt((x - 0) ** 2 + (y - 0) ** 2),
    Math.sqrt((x - rect.width) ** 2 + (y - 0) ** 2),
    Math.sqrt((x - 0) ** 2 + (y - rect.height) ** 2),
    Math.sqrt((x - rect.width) ** 2 + (y - rect.height) ** 2)
  ) * 2;

  // 创建涟漪对象
  const ripple = {
    id: Date.now() + Math.random(),
    x,
    y,
    size,
  };

  // 添加涟漪
  ripples.value.push(ripple);

  // 动画完成后移除涟漪
  setTimeout(() => {
    const index = ripples.value.findIndex(r => r.id === ripple.id);
    if (index > -1) {
      ripples.value.splice(index, 1);
    }
  }, 600);
};
</script>

<style scoped>
@keyframes ripple {
  0% {
    transform: translate(-50%, -50%) scale(0);
    opacity: 0.6;
  }
  100% {
    transform: translate(-50%, -50%) scale(1);
    opacity: 0;
  }
}

.animate-ripple {
  animation: ripple 0.6s ease-out forwards;
}

/* 确保圆角继承 */
.rounded-inherit {
  border-radius: inherit;
}

/* 只针对这个组件去掉outline */
.ripple-button {
  outline: none !important;
}

.ripple-button:focus {
  outline: none !important;
}

.ripple-button:active {
  outline: none !important;
}

.ripple-button:focus-visible {
  outline: none !important;
}
</style>

 