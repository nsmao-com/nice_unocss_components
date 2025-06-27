<template>
  <div :class="groupClass">
    <!-- 标签 -->
    <label v-if="label" :class="labelClass">{{ label }}</label>
    
    <!-- OTP输入框组 -->
    <div :class="otpContainerClass">
      <input
        v-for="(digit, index) in digits"
        :key="index"
        :ref="(el) => setInputRef(el, index)"
        :value="password && digit ? '•' : digit"
        :disabled="disabled"
        :class="inputClass(index)"
        type="text"
        inputmode="numeric"
        maxlength="1"
        autocomplete="one-time-code"
        @input="handleInput(index, $event)"
        @keydown="handleKeyDown(index, $event)"
        @focus="handleFocus(index)"
        @blur="handleBlur(index)"
        @paste="handlePaste($event)"
      />
    </div>
    
    <!-- 帮助文本或错误信息 -->
    <div v-if="helpText || errorMessage || shouldShowError" :class="messageClass">
      <p v-if="errorMessage" class="text-red-600 text-sm">{{ errorMessage }}</p>
      <p v-else-if="shouldShowError && !errorMessage" class="text-red-600 text-sm">请输入完整的验证码</p>
      <p v-else-if="helpText" class="text-slate-500 text-sm">{{ helpText }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch, nextTick } from 'vue';

const props = defineProps({
  // 基础属性
  modelValue: {
    type: String,
    default: '',
  },
  label: {
    type: String,
    default: '',
  },
  length: {
    type: Number,
    default: 6,
    validator: (value) => value >= 1 && value <= 10,
  },
  
  // 状态
  disabled: {
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
    validator: (value) => ['default', 'primary', 'success', 'warning', 'danger'].includes(value),
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  
  // 验证
  type: {
    type: String,
    default: 'numeric',
    validator: (value) => ['numeric', 'text', 'alphanumeric'].includes(value),
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
  
  // 行为
  autoFocus: {
    type: Boolean,
    default: false,
  },
  secure: {
    type: Boolean,
    default: false,
  },
  
  // 样式选项
  rounded: {
    type: Boolean,
    default: false,
  },
  password: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:modelValue', 'complete', 'focus', 'blur', 'change']);

// 状态
const digits = ref(Array(props.length).fill(''));
const inputRefs = ref([]);
const focusedIndex = ref(-1);
const hasBlurred = ref(false); // 是否已经失焦过

// 设置输入框引用
const setInputRef = (el, index) => {
  if (el) {
    inputRefs.value[index] = el;
  }
};

// 监听modelValue变化，同步到digits
watch(() => props.modelValue, (newValue) => {
  const valueArray = (newValue || '').split('').slice(0, props.length);
  digits.value = [...valueArray, ...Array(props.length - valueArray.length).fill('')];
  
  // 如果外部清空了值，重置失焦状态
  if (!newValue) {
    hasBlurred.value = false;
  }
}, { immediate: true });

// 监听digits变化，发出事件
watch(digits, (newDigits) => {
  const value = newDigits.join('');
  emit('update:modelValue', value);
  emit('change', value);
  
  // 检查是否完成输入
  if (value.length === props.length && !value.includes('')) {
    emit('complete', value);
    // 输入完整时重置错误状态
    hasBlurred.value = false;
  }
}, { deep: true });

// 计算是否应该显示错误状态
const shouldShowError = computed(() => {
  if (props.error) return true; // 手动设置的错误状态优先
  
  // 只有在失焦过并且输入不完整时才显示错误
  if (hasBlurred.value) {
    const value = digits.value.join('');
    return value.length > 0 && value.length < props.length;
  }
  
  return false;
});

// 计算是否输入完整
const isComplete = computed(() => {
  const value = digits.value.join('');
  return value.length === props.length && !value.includes('');
});

// 自动聚焦
watch(() => props.autoFocus, (shouldFocus) => {
  if (shouldFocus && inputRefs.value[0]) {
    nextTick(() => {
      inputRefs.value[0].focus();
    });
  }
}, { immediate: true });

// 输入验证
const isValidInput = (value) => {
  switch (props.type) {
    case 'numeric':
      return /^\d$/.test(value);
    case 'text':
      return /^[a-zA-Z]$/.test(value);
    case 'alphanumeric':
      return /^[a-zA-Z0-9]$/.test(value);
    default:
      return true;
  }
};

// 样式计算
const groupClass = computed(() => [
  'group relative',
  {
    'opacity-50': props.disabled,
  },
]);

const labelClass = computed(() => [
  'block text-sm font-medium text-slate-700 mb-2',
]);

const otpContainerClass = computed(() => {
  const baseClasses = ['flex items-center justify-center gap-2'];
  
  // 根据尺寸调整间距
  switch (props.size) {
    case 'sm':
      baseClasses.push('gap-1.5');
      break;
    case 'lg':
      baseClasses.push('gap-3');
      break;
    default:
      baseClasses.push('gap-2');
  }
  
  return baseClasses;
});

const inputClass = computed(() => (index) => {
  const baseClasses = [
    'flex items-center justify-center text-center font-medium',
    'border border-slate-200',
    'transition-all duration-200 ease-out',
    'focus:outline-none focus:ring-0',
    'bg-white',
  ];
  
  // 圆角样式
  if (props.rounded) {
    baseClasses.push('rounded-full');
  } else {
    baseClasses.push('rounded-lg');
  }
  
  // 尺寸
  switch (props.size) {
    case 'sm':
      baseClasses.push('w-8 h-8 text-sm');
      break;
    case 'lg':
      baseClasses.push('w-14 h-14 text-lg');
      break;
    default:
      baseClasses.push('w-12 h-12 text-base');
  }
  
  // 状态颜色
  if (props.disabled) {
    baseClasses.push('bg-slate-100 cursor-not-allowed text-slate-400');
  } else {
    // 检查错误状态（使用计算后的错误状态）
    if (shouldShowError.value || props.errorMessage) {
      baseClasses.push(
        'border-red-300 bg-red-50 text-red-900',
        'focus:border-red-500 focus:bg-red-50'
      );
    } else if (digits.value[index] && focusedIndex.value !== index) {
      // 有值且未聚焦时的成功状态
      switch (props.variant) {
        case 'primary':
          baseClasses.push('border-blue-300 bg-blue-50 text-blue-900');
          break;
        case 'success':
          baseClasses.push('border-green-300 bg-green-50 text-green-900');
          break;
        case 'warning':
          baseClasses.push('border-amber-300 bg-amber-50 text-amber-900');
          break;
        case 'danger':
          baseClasses.push('border-red-300 bg-red-50 text-red-900');
          break;
        default:
          baseClasses.push('border-slate-300 bg-slate-50 text-slate-900');
      }
    } else if (focusedIndex.value === index) {
      // 聚焦状态
      switch (props.variant) {
        case 'primary':
          baseClasses.push('border-blue-500 bg-blue-50 ring-4 ring-blue-100');
          break;
        case 'success':
          baseClasses.push('border-green-500 bg-green-50 ring-4 ring-green-100');
          break;
        case 'warning':
          baseClasses.push('border-amber-500 bg-amber-50 ring-4 ring-amber-100');
          break;
        case 'danger':
          baseClasses.push('border-red-500 bg-red-50 ring-4 ring-red-100');
          break;
        default:
          baseClasses.push('border-blue-500 bg-blue-50 ring-4 ring-blue-100');
      }
    } else {
      // 默认状态
      baseClasses.push(
        'border-slate-200 text-slate-900',
        'hover:border-slate-300 hover:bg-slate-50'
      );
    }
  }
  
  return baseClasses;
});

const messageClass = computed(() => [
  'mt-2 text-center',
]);

// 事件处理
const handleInput = (index, event) => {
  if (props.disabled) return;
  
  const value = event.target.value;
  
  // 只保留最后一个字符
  const lastChar = value.slice(-1);
  
  if (lastChar === '' || isValidInput(lastChar)) {
    // 更新当前位置的值
    digits.value[index] = lastChar;
    
    // 如果输入了有效字符，自动移动到下一个输入框
    if (lastChar && index < props.length - 1) {
      nextTick(() => {
        inputRefs.value[index + 1]?.focus();
      });
    }
  } else {
    // 如果输入无效，恢复原值
    event.target.value = digits.value[index];
  }
};

const handleKeyDown = (index, event) => {
  if (props.disabled) return;
  
  switch (event.key) {
    case 'Backspace':
      if (!digits.value[index] && index > 0) {
        // 如果当前框为空，删除前一个框的内容并聚焦
        digits.value[index - 1] = '';
        nextTick(() => {
          inputRefs.value[index - 1]?.focus();
        });
      } else {
        // 删除当前框的内容
        digits.value[index] = '';
      }
      break;
      
    case 'ArrowLeft':
      event.preventDefault();
      if (index > 0) {
        inputRefs.value[index - 1]?.focus();
      }
      break;
      
    case 'ArrowRight':
      event.preventDefault();
      if (index < props.length - 1) {
        inputRefs.value[index + 1]?.focus();
      }
      break;
      
    case 'Delete':
      digits.value[index] = '';
      break;
      
    case 'Home':
      event.preventDefault();
      inputRefs.value[0]?.focus();
      break;
      
    case 'End':
      event.preventDefault();
      inputRefs.value[props.length - 1]?.focus();
      break;
  }
};

const handleFocus = (index) => {
  focusedIndex.value = index;
  emit('focus', index);
};

const handleBlur = (index) => {
  focusedIndex.value = -1;
  hasBlurred.value = true; // 标记已经失焦过
  emit('blur', index);
};

const handlePaste = (event) => {
  if (props.disabled) return;
  
  event.preventDefault();
  const pastedData = event.clipboardData.getData('text');
  
  // 过滤并验证粘贴的数据
  const validChars = pastedData.split('').filter(char => isValidInput(char));
  
  // 从当前聚焦位置开始填充
  const startIndex = Math.max(0, focusedIndex.value);
  
  for (let i = 0; i < validChars.length && startIndex + i < props.length; i++) {
    digits.value[startIndex + i] = validChars[i];
  }
  
  // 聚焦到最后填充的位置或下一个空位置
  const nextIndex = Math.min(startIndex + validChars.length, props.length - 1);
  nextTick(() => {
    inputRefs.value[nextIndex]?.focus();
  });
};

// 公开方法
defineExpose({
  focus: () => {
    inputRefs.value[0]?.focus();
  },
  clear: () => {
    digits.value = Array(props.length).fill('');
    hasBlurred.value = false; // 清空时重置失焦状态
    inputRefs.value[0]?.focus();
  },
  reset: () => {
    digits.value = Array(props.length).fill('');
    hasBlurred.value = false;
  },
});
</script> 