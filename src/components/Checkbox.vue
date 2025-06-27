<template>
  <label :class="wrapperClass">
    <input
      type="checkbox"
      :checked="modelValue"
      :disabled="disabled"
      :value="value"
      @change="handleChange"
      class="sr-only"
    />
    
    <!-- 复选框容器 -->
    <div :class="checkboxContainerClass" :style="containerDynamicStyle">
      <!-- 勾选标记 -->
      <svg
        :class="checkmarkClass"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        class="relative z-10"
      >
        <path
          d="M3.5 8.5L6.5 11.5L12.5 5.5"
          stroke="white"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          fill="none"
          :style="checkmarkStyle"
        />
      </svg>
    </div>
    
    <!-- 标签文字 -->
    <span v-if="label || $slots.default" :class="labelClass">
      <slot>{{ label }}</slot>
    </span>
  </label>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const props = defineProps({
  // 绑定值
  modelValue: {
    type: Boolean,
    default: false,
  },
  // 复选框标签
  label: {
    type: String,
    default: '',
  },
  // 复选框值
  value: {
    type: [String, Number, Boolean],
    default: true,
  },
  // 是否禁用
  disabled: {
    type: Boolean,
    default: false,
  },
  // 颜色变体
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['default', 'primary', 'secondary', 'success', 'warning', 'danger'].includes(value),
  },
  // 大小
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  // 是否为圆形
  rounded: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:modelValue', 'change']);

// 动画状态
const animationProgress = ref(0);
const backgroundScale = ref(0);

// 处理变化事件
const handleChange = (event) => {
  const checked = event.target.checked;
  emit('update:modelValue', checked);
  emit('change', checked, props.value);
};

// 容器样式
const wrapperClass = computed(() => [
  'inline-flex items-center cursor-pointer',
  {
    'opacity-50 cursor-not-allowed': props.disabled,
  },
]);

// 复选框容器样式
const checkboxContainerClass = computed(() => {
  const classes = [
    'relative flex items-center justify-center border-2 overflow-hidden',
    'focus-within:ring-2 focus-within:ring-offset-2',
    'transition-colors duration-300 ease-out', // 改为transition-colors
  ];

  // 大小
  switch (props.size) {
    case 'sm':
      classes.push('w-4 h-4');
      break;
    case 'md':
      classes.push('w-5 h-5');
      break;
    case 'lg':
      classes.push('w-6 h-6');
      break;
  }

  // 形状
  if (props.rounded) {
    classes.push('rounded-full');
  } else {
    classes.push('rounded-md');
  }

  // 边框颜色和focus ring - 背景色在动态样式中设置
  if (props.modelValue) {
    // 选中状态的边框
    switch (props.variant) {
      case 'default':
        classes.push('border-slate-600 focus-within:ring-slate-500');
        break;
      case 'primary':
        classes.push('border-blue-600 focus-within:ring-blue-500');
        break;
      case 'secondary':
        classes.push('border-slate-500 focus-within:ring-slate-400');
        break;
      case 'success':
        classes.push('border-green-600 focus-within:ring-green-500');
        break;
      case 'warning':
        classes.push('border-amber-600 focus-within:ring-amber-500');
        break;
      case 'danger':
        classes.push('border-red-600 focus-within:ring-red-500');
        break;
    }
  } else {
    // 未选中状态
    classes.push('border-slate-300 hover:border-slate-400 focus-within:ring-blue-500');
  }

  return classes;
});



// 容器动态样式 - 只设置背景色，不缩放容器
const containerDynamicStyle = computed(() => {
  // 获取背景颜色
  const getBackgroundColor = () => {
    if (!props.modelValue) {
      return 'white';
    }
    
    // 根据动画进度计算背景色的透明度
    const alpha = backgroundScale.value;
    
    switch (props.variant) {
      case 'default':
        return `rgba(71, 85, 105, ${alpha})`; // slate-600
      case 'primary':
        return `rgba(37, 99, 235, ${alpha})`; // blue-600
      case 'secondary':
        return `rgba(100, 116, 139, ${alpha})`; // slate-500
      case 'success':
        return `rgba(22, 163, 74, ${alpha})`; // green-600
      case 'warning':
        return `rgba(217, 119, 6, ${alpha})`; // amber-600
      case 'danger':
        return `rgba(220, 38, 38, ${alpha})`; // red-600
      default:
        return `rgba(37, 99, 235, ${alpha})`;
    }
  };

  return {
    backgroundColor: getBackgroundColor(),
  };
});



// 勾选标记样式
const checkmarkClass = computed(() => {
  const classes = ['transition-all duration-300 ease-out relative z-10'];
  
  // 大小
  switch (props.size) {
    case 'sm':
      classes.push('w-3 h-3');
      break;
    case 'md':
      classes.push('w-4 h-4');
      break;
    case 'lg':
      classes.push('w-5 h-5');
      break;
  }

  return classes;
});

// 勾选标记动画样式
const checkmarkStyle = computed(() => {
  if (!props.modelValue) {
    return {
      strokeDasharray: '12',
      strokeDashoffset: '12',
      opacity: '0',
    };
  }
  
  return {
    strokeDasharray: '12',
    strokeDashoffset: `${12 - (animationProgress.value * 12)}`,
    opacity: '1',
  };
});

// 标签样式
const labelClass = computed(() => {
  const classes = ['select-none transition-colors duration-200'];
  
  // 大小
  switch (props.size) {
    case 'sm':
      classes.push('ml-2 text-sm');
      break;
    case 'md':
      classes.push('ml-2.5 text-base');
      break;
    case 'lg':
      classes.push('ml-3 text-lg');
      break;
  }

  // 颜色
  if (props.disabled) {
    classes.push('text-slate-400');
  } else {
    classes.push('text-slate-700');
  }

  return classes;
});

// 监听选中状态变化，触发动画
watch(() => props.modelValue, (newVal) => {
  if (newVal) {
    // 选中动画：先背景展开，然后打钩
    backgroundScale.value = 0;
    animationProgress.value = 0;
    
    const startTime = Date.now();
    const backgroundDuration = 200; // 背景展开动画时长
    const checkmarkDelay = 100; // 勾选动画延迟
    const checkmarkDuration = 300; // 勾选动画时长

    const animate = () => {
      const elapsed = Date.now() - startTime;
      
      // 背景缩放动画 (0-200ms)
      if (elapsed <= backgroundDuration) {
        const progress = elapsed / backgroundDuration;
        backgroundScale.value = progress < 0.5 
          ? 2 * progress * progress 
          : 1 - Math.pow(-2 * progress + 2, 2) / 2;
      } else {
        backgroundScale.value = 1;
      }
      
      // 勾选动画 (100-400ms)
      if (elapsed >= checkmarkDelay) {
        const checkmarkElapsed = elapsed - checkmarkDelay;
        if (checkmarkElapsed <= checkmarkDuration) {
          const progress = checkmarkElapsed / checkmarkDuration;
          animationProgress.value = progress < 0.5 
            ? 2 * progress * progress 
            : 1 - Math.pow(-2 * progress + 2, 2) / 2;
        } else {
          animationProgress.value = 1;
        }
      }
      
      if (elapsed < backgroundDuration + checkmarkDuration) {
        requestAnimationFrame(animate);
      }
    };
    
    requestAnimationFrame(animate);
  } else {
    // 取消选中动画：背景收缩消失
    animationProgress.value = 0;
    
    const startTime = Date.now();
    const duration = 200; // 背景收缩动画时长

    const animate = () => {
      const elapsed = Date.now() - startTime;
      const progress = Math.min(elapsed / duration, 1);
      
      // 从1缩放到0
      backgroundScale.value = 1 - (progress < 0.5 
        ? 2 * progress * progress 
        : 1 - Math.pow(-2 * progress + 2, 2) / 2);
      
      if (progress < 1) {
        requestAnimationFrame(animate);
      } else {
        backgroundScale.value = 0;
      }
    };
    
    requestAnimationFrame(animate);
  }
}, { immediate: true });
</script>

<style scoped>
/* 隐藏原生复选框但保持可访问性 */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
</style> 