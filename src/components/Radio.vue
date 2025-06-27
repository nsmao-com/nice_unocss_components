<template>
  <label :class="wrapperClass">
    <input
      type="radio"
      :checked="isChecked"
      :disabled="disabled"
      :value="value"
      :name="name"
      @change="handleChange"
      class="sr-only"
    />
    
    <!-- 单选框容器 -->
    <div :class="radioContainerClass" :style="containerDynamicStyle">
      <!-- 选中圆点 -->
      <div
        v-if="isChecked"
        :class="dotClass"
        :style="dotStyle"
      ></div>
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
    type: [String, Number, Boolean],
    default: null,
  },
  // 单选框标签
  label: {
    type: String,
    default: '',
  },
  // 单选框值
  value: {
    type: [String, Number, Boolean],
    required: true,
  },
  // 分组名称
  name: {
    type: String,
    default: '',
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
});

const emit = defineEmits(['update:modelValue', 'change']);

// 动画状态
const backgroundScale = ref(0);
const dotScale = ref(0);

// 是否选中
const isChecked = computed(() => props.modelValue === props.value);

// 处理变化事件
const handleChange = (event) => {
  if (event.target.checked) {
    emit('update:modelValue', props.value);
    emit('change', props.value);
  }
};

// 容器样式
const wrapperClass = computed(() => [
  'inline-flex items-center cursor-pointer',
  {
    'opacity-50 cursor-not-allowed': props.disabled,
  },
]);

// 单选框容器样式
const radioContainerClass = computed(() => {
  const classes = [
    'relative flex items-center justify-center border-2 rounded-full overflow-hidden',
    'focus-within:ring-2 focus-within:ring-offset-2',
    'transition-colors duration-300 ease-out',
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

  // 边框颜色和focus ring
  if (isChecked.value) {
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

// 容器动态样式 - 背景色动画
const containerDynamicStyle = computed(() => {
  const getBackgroundColor = () => {
    if (!isChecked.value) {
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

// 圆点样式
const dotClass = computed(() => {
  const classes = ['absolute rounded-full bg-white transition-all duration-300 ease-out'];
  
  // 大小 - 圆点比容器小
  switch (props.size) {
    case 'sm':
      classes.push('w-1.5 h-1.5');
      break;
    case 'md':
      classes.push('w-2 h-2');
      break;
    case 'lg':
      classes.push('w-2.5 h-2.5');
      break;
  }

  return classes;
});

// 圆点动画样式
const dotStyle = computed(() => {
  return {
    transform: `scale(${dotScale.value})`,
    transformOrigin: 'center',
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
watch(() => isChecked.value, (newVal) => {
  if (newVal) {
    // 选中动画：先背景填充，然后圆点出现
    backgroundScale.value = 0;
    dotScale.value = 0;
    
    const startTime = Date.now();
    const backgroundDuration = 200; // 背景填充动画时长
    const dotDelay = 100; // 圆点动画延迟
    const dotDuration = 200; // 圆点动画时长

    const animate = () => {
      const elapsed = Date.now() - startTime;
      
      // 背景填充动画 (0-200ms)
      if (elapsed <= backgroundDuration) {
        const progress = elapsed / backgroundDuration;
        backgroundScale.value = progress < 0.5 
          ? 2 * progress * progress 
          : 1 - Math.pow(-2 * progress + 2, 2) / 2;
      } else {
        backgroundScale.value = 1;
      }
      
      // 圆点动画 (100-300ms)
      if (elapsed >= dotDelay) {
        const dotElapsed = elapsed - dotDelay;
        if (dotElapsed <= dotDuration) {
          const progress = dotElapsed / dotDuration;
          dotScale.value = progress < 0.5 
            ? 2 * progress * progress 
            : 1 - Math.pow(-2 * progress + 2, 2) / 2;
        } else {
          dotScale.value = 1;
        }
      }
      
      if (elapsed < backgroundDuration + dotDuration) {
        requestAnimationFrame(animate);
      }
    };
    
    requestAnimationFrame(animate);
  } else {
    // 取消选中动画：圆点和背景同时消失
    const startTime = Date.now();
    const duration = 150; // 动画时长

    const animate = () => {
      const elapsed = Date.now() - startTime;
      const progress = Math.min(elapsed / duration, 1);
      
      // 从1缩放到0
      const scale = 1 - (progress < 0.5 
        ? 2 * progress * progress 
        : 1 - Math.pow(-2 * progress + 2, 2) / 2);
      
      backgroundScale.value = scale;
      dotScale.value = scale;
      
      if (progress < 1) {
        requestAnimationFrame(animate);
      } else {
        backgroundScale.value = 0;
        dotScale.value = 0;
      }
    };
    
    requestAnimationFrame(animate);
  }
}, { immediate: true });
</script>

<style scoped>
/* 隐藏原生单选框但保持可访问性 */
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