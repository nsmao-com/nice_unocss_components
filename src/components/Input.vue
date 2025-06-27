<template>
  <div :class="groupClass">
    <!-- 固定标签模式 - label在输入框外部 -->
    <label 
      v-if="label && description"
      :for="inputId" 
      :class="fixedLabelClass"
    >
      {{ label }}
    </label>
    
    <!-- 输入框包装器 -->
    <div 
      :class="inputWrapperClass" 
      @click="focusInput"
      style="cursor: text;"
    >
      <!-- 浮动标签 - 只在无description时显示 -->
      <label 
        v-if="label && !description"
        :for="inputId" 
        :class="floatingLabelClass"
      >
        {{ label }}
      </label>
      
      <!-- 内部包装器 -->
      <div :class="innerWrapperClass">
        <!-- 前置图标 -->
        <div v-if="prefixIcon" :class="prefixIconClass">
          <component :is="prefixIcon" :size="iconSize" />
        </div>
        
        <!-- 输入框 -->
        <input
          :id="inputId"
          :type="type"
          :value="modelValue"
          :placeholder="computedPlaceholder"
          :disabled="disabled"
          :readonly="readonly"
          :class="inputClass"
          @input="handleInput"
          @focus="handleFocus"
          @blur="handleBlur"
          @change="handleChange"
          ref="inputRef"
        />
        
        <!-- 验证图标 -->
        <div v-if="shouldShowValidationIcon" :class="validationIconClass">
          <Check v-if="validationStatus === true" :size="iconSize" />
          <AlertCircle v-else-if="validationStatus === false" :size="iconSize" />
        </div>
        
        <!-- 后置图标 -->
        <div v-if="suffixIcon" :class="suffixIconClass">
          <component :is="suffixIcon" :size="iconSize" />
        </div>
        
        <!-- 清除按钮 -->
        <button
          v-if="clearable && modelValue && !disabled"
          @click="handleClear"
          :class="clearButtonClass"
          type="button"
        >
          <X :size="14" />
        </button>
      </div>
    </div>
    
    <!-- 帮助文本或错误信息 -->
    <div v-if="helpText || computedErrorMessage" :class="messageClass">
      <p v-if="computedErrorMessage" class="text-red-600 text-sm">{{ computedErrorMessage }}</p>
      <p v-else-if="helpText" class="text-slate-500 text-sm">{{ helpText }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, nextTick } from 'vue';
import { X, Check, AlertCircle } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  modelValue: {
    type: [String, Number],
    default: '',
  },
  label: {
    type: String,
    default: '',
  },
  description: {
    type: String,
    default: '',
  },
  placeholder: {
    type: String,
    default: '',
  },
  type: {
    type: String,
    default: 'text',
  },
  
  // 状态
  disabled: {
    type: Boolean,
    default: false,
  },
  readonly: {
    type: Boolean,
    default: false,
  },
  error: {
    type: Boolean,
    default: false,
  },
  
  // 样式
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'primary', 'secondary', 'success', 'warning', 'danger'].includes(value),
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  
  // 验证
  validationType: {
    type: String,
    default: '',
    validator: (value) => ['', 'email', 'phone', 'url', 'number', 'password'].includes(value),
  },
  showValidationIcon: {
    type: Boolean,
    default: true,
  },
  
  // 功能
  clearable: {
    type: Boolean,
    default: false,
  },
  prefixIcon: {
    type: [String, Object, Function],
    default: null,
  },
  suffixIcon: {
    type: [String, Object, Function],
    default: null,
  },
  
  // 消息
  helpText: {
    type: String,
    default: '',
  },
  errorMessage: {
    type: String,
    default: '',
  },
});

const emit = defineEmits(['update:modelValue', 'focus', 'blur', 'change', 'clear']);

// 状态
const isFocused = ref(false);
const inputRef = ref(null);

// 生成唯一ID
const inputId = computed(() => `input-${Math.random().toString(36).substr(2, 9)}`);

// 图标大小
const iconSize = computed(() => {
  switch (props.size) {
    case 'sm': return 16;
    case 'md': return 18;
    case 'lg': return 20;
    default: return 18;
  }
});

// 是否有值或聚焦（填充状态）- 用于浮动标签模式
const hasValueOrFocus = computed(() => {
  return isFocused.value || (props.modelValue !== '' && props.modelValue !== null && props.modelValue !== undefined);
});

// 是否为浮动标签模式
const isFloatingLabelMode = computed(() => {
  return props.label && !props.description;
});

// 是否为固定标签模式
const isFixedLabelMode = computed(() => {
  return props.label && props.description;
});

// 验证逻辑和错误信息
const validationRules = {
  email: {
    validate: (value) => {
      if (!value) return null;
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(value);
    },
    errorMessage: '请输入有效的邮箱地址'
  },
  phone: {
    validate: (value) => {
      if (!value) return null;
      const phoneRegex = /^[+]?[\d\s\-\(\)]+$/;
      const digitsOnly = value.replace(/\D/g, '');
      return phoneRegex.test(value) && digitsOnly.length >= 10;
    },
    errorMessage: '请输入有效的电话号码'
  },
  url: {
    validate: (value) => {
      if (!value) return null;
      try {
        new URL(value);
        return true;
      } catch {
        return false;
      }
    },
    errorMessage: '请输入有效的网址'
  },
  number: {
    validate: (value) => {
      if (!value) return null;
      return !isNaN(Number(value)) && isFinite(Number(value));
    },
    errorMessage: '请输入有效的数字'
  },
  password: {
    validate: (value) => {
      if (!value) return null;
      // 密码验证：至少6位，包含字母和数字
      return value.length >= 6 && /[a-zA-Z]/.test(value) && /\d/.test(value);
    },
    errorMessage: '密码至少6位，需包含字母和数字'
  },
};

// 验证状态
const validationStatus = computed(() => {
  if (!props.validationType) return null;
  
  const rule = validationRules[props.validationType];
  if (!rule) return null;
  
  return rule.validate(props.modelValue);
});

// 是否显示验证图标
const shouldShowValidationIcon = computed(() => {
  // 有验证类型且有值时显示图标
  return props.showValidationIcon && props.validationType && props.modelValue && props.modelValue.length > 0;
});

// 计算占位符 - 区分两种模式
const computedPlaceholder = computed(() => {
  // 固定标签模式：有description时，description作为placeholder
  if (props.description) {
    return props.description;
  }
  
  // 浮动标签模式：有标签但无description时，只在聚焦或有值时显示placeholder
  if (props.label && !props.description) {
    return hasValueOrFocus.value ? props.placeholder : '';
  }
  
  // 无标签模式：直接显示placeholder
  return props.placeholder;
});

// 计算最终的错误信息
const computedErrorMessage = computed(() => {
  // 如果手动设置了错误信息，优先使用
  if (props.errorMessage) return props.errorMessage;
  
  // 如果有验证类型且验证失败，显示默认错误信息
  if (props.validationType && validationStatus.value === false) {
    const rule = validationRules[props.validationType];
    return rule ? rule.errorMessage : '';
  }
  
  return '';
});

// 外层组容器样式
const groupClass = computed(() => [
  'group relative',
  {
    'opacity-50': props.disabled,
  },
]);

// 输入框包装器样式 - 直接仿照NextUI
const inputWrapperClass = computed(() => {
  const baseClasses = [
    'relative w-full inline-flex tap-highlight-transparent shadow-sm px-3',
    'flex-col items-start justify-center gap-0 transition-background',
    'motion-reduce:transition-none !duration-150 outline-none',
    'rounded-[12px]', // 使用12px圆角
  ];

  // 固定高度 - 直接仿照NextUI的h-14
  baseClasses.push('min-h-14 h-14 py-2');

  // 背景和悬停效果 - 根据验证状态调整
  if (props.disabled) {
    baseClasses.push('bg-slate-100 cursor-not-allowed');
  } else {
    // 检查错误状态
    if (props.error || computedErrorMessage.value) {
      // 错误状态
      baseClasses.push('bg-red-50 hover:bg-red-100 focus-within:bg-red-50 border border-red-200');
    } else if (shouldShowValidationIcon.value && validationStatus.value === true) {
      // 验证成功
      baseClasses.push('bg-green-50 hover:bg-green-100 focus-within:bg-green-50 border border-green-200');
    } else if (shouldShowValidationIcon.value && validationStatus.value === false) {
      // 验证失败
      baseClasses.push('bg-red-50 hover:bg-red-100 focus-within:bg-red-50 border border-red-200');
    } else {
      // 默认状态
      baseClasses.push('bg-[#F4F4F5] hover:bg-[#EEEEEF] focus-within:bg-[#F4F4F5]');
    }
  }

  return baseClasses;
});

// 固定标签样式 - 在输入框外部
const fixedLabelClass = computed(() => [
  'block text-sm font-medium text-slate-700 mb-1',
]);

// 浮动标签样式 - 使用transform实现平滑动画，移动到左上角
const floatingLabelClass = computed(() => {
  const baseClasses = [
    'absolute z-10 pointer-events-none origin-top-left',
    'block cursor-text',
    'duration-200 ease-out',
    'transition-all', // 过渡所有属性
    'pr-2 max-w-full overflow-hidden',
    'top-1/2', // 始终基于中央定位
    'transform', // 确保transform生效
    'select-none', // 防止标签被选中
  ];

  // 根据是否有前置图标调整左边距
  if (props.prefixIcon) {
    baseClasses.push('left-11'); // 有图标时，标签位置右移，避免重合
  } else {
    baseClasses.push('left-3'); // 无图标时，正常左边距
  }

  // 根据是否有值或聚焦来确定状态（仅用于浮动标签模式）
  if (hasValueOrFocus.value) {
    // 激活状态：移动到左上角，缩放到视觉12px
    let textColor = 'text-slate-600'; // 默认填充状态颜色
    
    // 检查错误状态
    if (props.error || computedErrorMessage.value) {
      textColor = 'text-red-600';
    } else if (isFocused.value) {
      switch (props.variant) {
        case 'primary': textColor = 'text-blue-600'; break;
        case 'secondary': textColor = 'text-slate-600'; break;
        case 'success': textColor = 'text-green-600'; break;
        case 'warning': textColor = 'text-amber-600'; break;
        case 'danger': textColor = 'text-red-600'; break;
        default: textColor = 'text-slate-600'; break;
      }
    }
    
    baseClasses.push(
      textColor,
      'pointer-events-auto',
      'text-xs', // 更小的字体
      'scale-100', // 不缩放，直接使用小字体
      '-translate-y-4', // 减少向上移动的距离，让标签也下移一点
    );
    
    // 激活时，统一移动到左上角
    if (props.prefixIcon) {
      baseClasses.push('-translate-x-8'); // 有图标时，向左移动到正确位置
    }
  } else {
    // 默认状态：在输入框中央
    baseClasses.push(
      'text-slate-500', // 默认颜色
      'text-sm', // 基础14px字体大小
      'scale-100', // 正常大小
      '-translate-y-1/2', // 基准居中位置
    );
  }

  return baseClasses;
});

// 内部包装器样式 - 在浮动标签激活时添加上边距
const innerWrapperClass = computed(() => {
  const baseClasses = [
    'inline-flex w-full items-center h-full box-border',
  ];
  
  // 浮动标签模式下，激活时添加上边距，让输入框往下移动一点
  if (isFloatingLabelMode.value && hasValueOrFocus.value) {
    baseClasses.push('pt-5'); // 进一步增加上内边距，让整体内容更居中
  }
  
  return baseClasses;
});

// 输入框样式 - 直接仿照NextUI
const inputClass = computed(() => [
  'w-full font-normal bg-transparent !outline-none',
  'placeholder:text-slate-500', // foreground-500
  'focus-visible:outline-none',
  'autofill:bg-transparent bg-clip-text',
  'text-sm', // small size like NextUI
  'text-slate-900', // default-foreground when has value
  // 图标间距
  props.prefixIcon ? 'pl-1.5' : '', // 改为pl-1.5
  (props.suffixIcon || props.clearable || shouldShowValidationIcon.value) ? 'pr-1.5' : '', // 考虑验证图标
].filter(Boolean));

// 前置图标样式 - 保持固定位置
const prefixIconClass = computed(() => {
  return [
    'flex items-center text-slate-500 mr-2',
    // 不再根据浮动标签状态移动，保持固定位置
  ];
});

// 验证图标样式 - 保持固定位置
const validationIconClass = computed(() => {
  return [
    'flex items-center ml-2',
    validationStatus.value ? 'text-green-500' : 'text-red-500',
    // 不再根据浮动标签状态移动，保持固定位置
  ];
});

// 后置图标样式 - 保持固定位置
const suffixIconClass = computed(() => {
  return [
    'flex items-center text-slate-500 ml-2',
    // 不再根据浮动标签状态移动，保持固定位置
  ];
});

// 清除按钮样式 - 保持固定位置
const clearButtonClass = computed(() => {
  return [
    'flex items-center text-slate-400 hover:text-slate-600 ml-2',
    'focus:outline-none transition-colors duration-200', // 只保留颜色过渡
    // 不再根据浮动标签状态移动，保持固定位置
  ];
});

// 消息样式
const messageClass = computed(() => [
  'mt-1',
]);

// 事件处理
const handleInput = (event) => {
  emit('update:modelValue', event.target.value);
};

const handleFocus = (event) => {
  isFocused.value = true;
  emit('focus', event);
};

const handleBlur = (event) => {
  isFocused.value = false;
  emit('blur', event);
};

const handleChange = (event) => {
  emit('change', event);
};

const handleClear = () => {
  emit('update:modelValue', '');
  emit('clear');
  nextTick(() => {
    inputRef.value?.focus();
  });
};

// 点击容器时聚焦输入框
const focusInput = () => {
  if (!props.disabled) {
    inputRef.value?.focus();
  }
};
</script>

<style scoped>
</style> 