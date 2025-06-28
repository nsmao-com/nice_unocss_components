<template>
  <div 
    class="popover-wrapper relative inline-block"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
    @click="handleClick"
  >
    <!-- 触发元素 -->
    <div 
      ref="triggerRef"
      :class="triggerClass"
      :aria-expanded="isVisible"
      :aria-describedby="isVisible ? popoverId : undefined"
      role="button"
      :tabindex="disabled ? -1 : 0"
      @keydown="handleKeydown"
    >
      <slot name="trigger">
        <button 
          :class="defaultTriggerClass"
          :disabled="disabled"
        >
          {{ triggerText }}
        </button>
      </slot>
    </div>

    <!-- 弹出框 -->
    <Teleport to="body">
      <Transition
        :name="transitionName"
        @enter="onEnter"
        @leave="onLeave"
      >
        <div
          v-if="isVisible"
          ref="popoverRef"
          :id="popoverId"
          :class="popoverClass"
          :style="popoverStyle"
          role="tooltip"
          @mouseenter="handlePopoverMouseEnter"
          @mouseleave="handlePopoverMouseLeave"
        >
          <!-- 箭头 -->
          <div 
            v-if="showArrow"
            :class="arrowClass"
            :style="arrowStyle"
          ></div>

          <!-- 内容区域 -->
          <div :class="contentClass">
            <!-- 标题 -->
            <div 
              v-if="title || $slots.title"
              :class="titleClass"
            >
              <slot name="title">{{ title }}</slot>
            </div>

            <!-- 内容 -->
            <div :class="bodyClass">
              <slot name="content">{{ content }}</slot>
            </div>

            <!-- 关闭按钮 -->
            <button
              v-if="closable"
              @click="hide"
              :class="closeButtonClass"
              aria-label="关闭"
            >
              <X :size="14" />
            </button>
          </div>
        </div>
      </Transition>
    </Teleport>

    <!-- 遮罩层 -->
    <Teleport to="body">
      <Transition name="fade">
        <div
          v-if="isVisible && showOverlay"
          class="fixed inset-0 z-40 bg-black/10"
          @click="hide"
        ></div>
      </Transition>
    </Teleport>
  </div>
</template>

<script setup>
import { computed, ref, nextTick, onMounted, onUnmounted, watch } from 'vue';
import { X } from 'lucide-vue-next';

const props = defineProps({
  // 内容
  title: {
    type: String,
    default: '',
  },
  content: {
    type: String,
    default: '',
  },
  triggerText: {
    type: String,
    default: 'Open Popover',
  },

  // 触发方式
  trigger: {
    type: String,
    default: 'click',
    validator: (value) => ['click', 'hover', 'manual'].includes(value),
  },

  // 位置
  placement: {
    type: String,
    default: 'top',
    validator: (value) => [
      'top', 'top-start', 'top-end',
      'bottom', 'bottom-start', 'bottom-end',
      'left', 'left-start', 'left-end',
      'right', 'right-start', 'right-end'
    ].includes(value),
  },

  // 样式
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'dark', 'light', 'primary'].includes(value),
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },

  // 功能选项
  disabled: {
    type: Boolean,
    default: false,
  },
  closable: {
    type: Boolean,
    default: false,
  },
  showArrow: {
    type: Boolean,
    default: true,
  },
  showOverlay: {
    type: Boolean,
    default: false,
  },

  // 延迟
  showDelay: {
    type: Number,
    default: 0,
  },
  hideDelay: {
    type: Number,
    default: 100,
  },

  // 偏移
  offset: {
    type: Number,
    default: 8,
  },

  // 宽度
  width: {
    type: [String, Number],
    default: 'auto',
  },
  maxWidth: {
    type: [String, Number],
    default: 320,
  },

  // 可见性控制
  visible: {
    type: Boolean,
    default: undefined,
  },
});

const emit = defineEmits(['update:visible', 'show', 'hide', 'toggle']);

// 响应式状态
const isVisible = ref(false);
const triggerRef = ref(null);
const popoverRef = ref(null);
const popoverPosition = ref({ top: 0, left: 0 });
const arrowPosition = ref({ top: 0, left: 0 });
const actualPlacement = ref(props.placement);

// 定时器
let showTimer = null;
let hideTimer = null;

// 唯一ID
const popoverId = `popover-${Math.random().toString(36).substr(2, 9)}`;

// 计算属性
const triggerClass = computed(() => [
  'popover-trigger',
  {
    'cursor-pointer': !props.disabled,
    'cursor-not-allowed opacity-50': props.disabled,
  }
]);

const defaultTriggerClass = computed(() => [
  'inline-flex items-center justify-center px-4 py-2 text-sm font-medium',
  'bg-white border border-slate-200 rounded-lg shadow-sm',
  'hover:bg-slate-50 hover:border-slate-300',
  'focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-1',
  'transition-colors duration-200',
  {
    'cursor-not-allowed opacity-50': props.disabled,
  }
]);

const popoverClass = computed(() => {
  const baseClasses = [
    'popover',
    'absolute z-50 rounded-lg shadow-lg border',
    'transform transition-all duration-200 ease-out',
  ];

  // 尺寸
  switch (props.size) {
    case 'sm':
      baseClasses.push('text-xs');
      break;
    case 'lg':
      baseClasses.push('text-base');
      break;
    default:
      baseClasses.push('text-sm');
  }

  // 变体
  switch (props.variant) {
    case 'dark':
      baseClasses.push('bg-slate-900 text-white border-slate-700');
      break;
    case 'light':
      baseClasses.push('bg-white text-slate-900 border-slate-100 shadow-xl');
      break;
    case 'primary':
      baseClasses.push('bg-blue-600 text-white border-blue-500');
      break;
    default:
      baseClasses.push('bg-white text-slate-900 border-slate-200');
  }

  return baseClasses;
});

const popoverStyle = computed(() => {
  const style = {
    top: `${popoverPosition.value.top}px`,
    left: `${popoverPosition.value.left}px`,
    width: props.width === 'auto' ? 'auto' : `${props.width}px`,
    maxWidth: `${props.maxWidth}px`,
  };
  return style;
});

const contentClass = computed(() => {
  const baseClasses = ['relative'];
  
  switch (props.size) {
    case 'sm':
      baseClasses.push('p-2');
      break;
    case 'lg':
      baseClasses.push('p-4');
      break;
    default:
      baseClasses.push('p-3');
  }

  return baseClasses;
});

const titleClass = computed(() => [
  'font-semibold mb-1',
  {
    'text-xs': props.size === 'sm',
    'text-sm': props.size === 'md',
    'text-base': props.size === 'lg',
  }
]);

const bodyClass = computed(() => [
  'popover-body',
  {
    'text-slate-600': props.variant === 'default' || props.variant === 'light',
    'text-slate-300': props.variant === 'dark',
    'text-blue-100': props.variant === 'primary',
  }
]);

const arrowClass = computed(() => {
  const baseClasses = ['popover-arrow', 'absolute', 'w-0', 'h-0'];
  
  // 箭头方向和颜色
  const placement = actualPlacement.value;
  
  if (placement.startsWith('top')) {
    baseClasses.push('border-l-4 border-r-4 border-t-4');
    baseClasses.push('border-l-transparent border-r-transparent');
    
    switch (props.variant) {
      case 'dark':
        baseClasses.push('border-t-slate-900');
        break;
      case 'primary':
        baseClasses.push('border-t-blue-600');
        break;
      default:
        baseClasses.push('border-t-white');
    }
  } else if (placement.startsWith('bottom')) {
    baseClasses.push('border-l-4 border-r-4 border-b-4');
    baseClasses.push('border-l-transparent border-r-transparent');
    
    switch (props.variant) {
      case 'dark':
        baseClasses.push('border-b-slate-900');
        break;
      case 'primary':
        baseClasses.push('border-b-blue-600');
        break;
      default:
        baseClasses.push('border-b-white');
    }
  } else if (placement.startsWith('left')) {
    baseClasses.push('border-t-4 border-b-4 border-l-4');
    baseClasses.push('border-t-transparent border-b-transparent');
    
    switch (props.variant) {
      case 'dark':
        baseClasses.push('border-l-slate-900');
        break;
      case 'primary':
        baseClasses.push('border-l-blue-600');
        break;
      default:
        baseClasses.push('border-l-white');
    }
  } else if (placement.startsWith('right')) {
    baseClasses.push('border-t-4 border-b-4 border-r-4');
    baseClasses.push('border-t-transparent border-b-transparent');
    
    switch (props.variant) {
      case 'dark':
        baseClasses.push('border-r-slate-900');
        break;
      case 'primary':
        baseClasses.push('border-r-blue-600');
        break;
      default:
        baseClasses.push('border-r-white');
    }
  }

  return baseClasses;
});

const arrowStyle = computed(() => ({
  top: `${arrowPosition.value.top}px`,
  left: `${arrowPosition.value.left}px`,
}));

const closeButtonClass = computed(() => {
  const baseClasses = [
    'absolute w-6 h-6 flex items-center justify-center',
    'rounded-full hover:bg-black/10 transition-colors duration-200'
  ];

  // 根据尺寸调整位置
  switch (props.size) {
    case 'sm':
      baseClasses.push('top-1 right-1');
      break;
    case 'lg':
      baseClasses.push('top-2 right-2');
      break;
    default:
      baseClasses.push('top-1.5 right-1.5');
  }

  // 根据变体调整颜色
  if (props.variant === 'dark' || props.variant === 'primary') {
    baseClasses.push('text-white hover:bg-white/20');
  } else {
    baseClasses.push('text-slate-400 hover:text-slate-600 hover:bg-slate-100');
  }

  return baseClasses;
});

const transitionName = computed(() => {
  const placement = actualPlacement.value;
  if (placement.startsWith('top')) return 'popover-top';
  if (placement.startsWith('bottom')) return 'popover-bottom';
  if (placement.startsWith('left')) return 'popover-left';
  if (placement.startsWith('right')) return 'popover-right';
  return 'popover-top';
});

// 方法
const show = async () => {
  if (props.disabled) return;
  
  clearTimeout(hideTimer);
  
  const showPopover = async () => {
    // 预先设置初始位置，避免飞入效果
    if (triggerRef.value) {
      const triggerRect = triggerRef.value.getBoundingClientRect();
      // 设置一个接近最终位置的初始位置
      popoverPosition.value = {
        top: triggerRect.top + window.scrollY - 50, // 预估位置
        left: triggerRect.left + window.scrollX
      };
    }
    
    isVisible.value = true;
    emit('update:visible', true);
    emit('show');
  };
  
  if (props.showDelay > 0) {
    showTimer = setTimeout(showPopover, props.showDelay);
  } else {
    await showPopover();
  }
};

const hide = () => {
  clearTimeout(showTimer);
  
  if (props.hideDelay > 0) {
    hideTimer = setTimeout(() => {
      isVisible.value = false;
      emit('update:visible', false);
      emit('hide');
    }, props.hideDelay);
  } else {
    isVisible.value = false;
    emit('update:visible', false);
    emit('hide');
  }
};

const toggle = () => {
  if (isVisible.value) {
    hide();
  } else {
    show();
  }
  emit('toggle', isVisible.value);
};

// 事件处理
const handleClick = () => {
  if (props.trigger === 'click') {
    toggle();
  }
};

const handleMouseEnter = () => {
  if (props.trigger === 'hover') {
    show();
  }
};

const handleMouseLeave = () => {
  if (props.trigger === 'hover') {
    hide();
  }
};

const handlePopoverMouseEnter = () => {
  if (props.trigger === 'hover') {
    clearTimeout(hideTimer);
  }
};

const handlePopoverMouseLeave = () => {
  if (props.trigger === 'hover') {
    hide();
  }
};

const handleKeydown = (event) => {
  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault();
    if (props.trigger === 'click') {
      toggle();
    }
  } else if (event.key === 'Escape') {
    hide();
  }
};

// 定位计算
const calculatePosition = () => {
  if (!triggerRef.value || !popoverRef.value) return;

  const triggerRect = triggerRef.value.getBoundingClientRect();
  const popoverRect = popoverRef.value.getBoundingClientRect();
  const viewport = {
    width: window.innerWidth,
    height: window.innerHeight,
  };

  let placement = props.placement;
  let top = 0;
  let left = 0;

  // 计算基础位置
  switch (placement) {
    case 'top':
    case 'top-start':
    case 'top-end':
      top = triggerRect.top - popoverRect.height - props.offset;
      break;
    case 'bottom':
    case 'bottom-start':
    case 'bottom-end':
      top = triggerRect.bottom + props.offset;
      break;
    case 'left':
    case 'left-start':
    case 'left-end':
      left = triggerRect.left - popoverRect.width - props.offset;
      break;
    case 'right':
    case 'right-start':
    case 'right-end':
      left = triggerRect.right + props.offset;
      break;
  }

  // 计算水平位置
  if (placement.includes('top') || placement.includes('bottom')) {
    if (placement.includes('start')) {
      left = triggerRect.left;
    } else if (placement.includes('end')) {
      left = triggerRect.right - popoverRect.width;
    } else {
      left = triggerRect.left + (triggerRect.width - popoverRect.width) / 2;
    }
  }

  // 计算垂直位置
  if (placement.includes('left') || placement.includes('right')) {
    if (placement.includes('start')) {
      top = triggerRect.top;
    } else if (placement.includes('end')) {
      top = triggerRect.bottom - popoverRect.height;
    } else {
      top = triggerRect.top + (triggerRect.height - popoverRect.height) / 2;
    }
  }

  // 边界检测和调整
  if (left < 8) {
    left = 8;
  } else if (left + popoverRect.width > viewport.width - 8) {
    left = viewport.width - popoverRect.width - 8;
  }

  if (top < 8) {
    // 如果上方空间不足，尝试翻转到下方
    if (placement.startsWith('top')) {
      top = triggerRect.bottom + props.offset;
      placement = placement.replace('top', 'bottom');
    } else {
      top = 8;
    }
  } else if (top + popoverRect.height > viewport.height - 8) {
    // 如果下方空间不足，尝试翻转到上方
    if (placement.startsWith('bottom')) {
      top = triggerRect.top - popoverRect.height - props.offset;
      placement = placement.replace('bottom', 'top');
    } else {
      top = viewport.height - popoverRect.height - 8;
    }
  }

  // 添加滚动偏移
  top += window.scrollY;
  left += window.scrollX;

  popoverPosition.value = { top, left };
  actualPlacement.value = placement;

  // 计算箭头位置
  calculateArrowPosition();
};

const calculateArrowPosition = () => {
  if (!props.showArrow || !triggerRef.value || !popoverRef.value) return;

  const triggerRect = triggerRef.value.getBoundingClientRect();
  const placement = actualPlacement.value;
  
  let arrowTop = 0;
  let arrowLeft = 0;

  if (placement.startsWith('top')) {
    arrowTop = popoverRef.value.offsetHeight;
    arrowLeft = Math.max(8, Math.min(
      popoverRef.value.offsetWidth - 16,
      (triggerRect.left + triggerRect.width / 2) - (popoverPosition.value.left - window.scrollX) - 4
    ));
  } else if (placement.startsWith('bottom')) {
    arrowTop = -4;
    arrowLeft = Math.max(8, Math.min(
      popoverRef.value.offsetWidth - 16,
      (triggerRect.left + triggerRect.width / 2) - (popoverPosition.value.left - window.scrollX) - 4
    ));
  } else if (placement.startsWith('left')) {
    arrowLeft = popoverRef.value.offsetWidth;
    arrowTop = Math.max(8, Math.min(
      popoverRef.value.offsetHeight - 16,
      (triggerRect.top + triggerRect.height / 2) - (popoverPosition.value.top - window.scrollY) - 4
    ));
  } else if (placement.startsWith('right')) {
    arrowLeft = -4;
    arrowTop = Math.max(8, Math.min(
      popoverRef.value.offsetHeight - 16,
      (triggerRect.top + triggerRect.height / 2) - (popoverPosition.value.top - window.scrollY) - 4
    ));
  }

  arrowPosition.value = { top: arrowTop, left: arrowLeft };
};

// 过渡事件
const onEnter = async (el) => {
  // 先隐藏元素，计算位置后再显示
  el.style.opacity = '0';
  await nextTick();
  calculatePosition();
  await nextTick();
  el.style.opacity = '1';
};

const onLeave = () => {
  // 清理
};

// 外部点击关闭
const handleOutsideClick = (event) => {
  if (
    isVisible.value &&
    triggerRef.value &&
    popoverRef.value &&
    !triggerRef.value.contains(event.target) &&
    !popoverRef.value.contains(event.target)
  ) {
    hide();
  }
};

// 监听器
watch(() => props.visible, (newVal) => {
  if (newVal !== undefined) {
    isVisible.value = newVal;
  }
});

watch(isVisible, () => {
  if (isVisible.value) {
    nextTick(() => calculatePosition());
  }
});

// 生命周期
onMounted(() => {
  document.addEventListener('click', handleOutsideClick);
  window.addEventListener('resize', calculatePosition);
  window.addEventListener('scroll', calculatePosition);
});

onUnmounted(() => {
  document.removeEventListener('click', handleOutsideClick);
  window.removeEventListener('resize', calculatePosition);
  window.removeEventListener('scroll', calculatePosition);
  clearTimeout(showTimer);
  clearTimeout(hideTimer);
});

// 暴露方法
defineExpose({
  show,
  hide,
  toggle,
});
</script>

<style scoped>
/* 过渡动画 */
.popover-top-enter-active,
.popover-top-leave-active {
  transition: all 0.15s ease-out;
}

.popover-top-enter-from {
  opacity: 0;
  transform: translateY(4px) scale(0.98);
}

.popover-top-leave-to {
  opacity: 0;
  transform: translateY(4px) scale(0.98);
}

.popover-bottom-enter-active,
.popover-bottom-leave-active {
  transition: all 0.15s ease-out;
}

.popover-bottom-enter-from {
  opacity: 0;
  transform: translateY(-4px) scale(0.98);
}

.popover-bottom-leave-to {
  opacity: 0;
  transform: translateY(-4px) scale(0.98);
}

.popover-left-enter-active,
.popover-left-leave-active {
  transition: all 0.15s ease-out;
}

.popover-left-enter-from {
  opacity: 0;
  transform: translateX(4px) scale(0.98);
}

.popover-left-leave-to {
  opacity: 0;
  transform: translateX(4px) scale(0.98);
}

.popover-right-enter-active,
.popover-right-leave-active {
  transition: all 0.15s ease-out;
}

.popover-right-enter-from {
  opacity: 0;
  transform: translateX(-4px) scale(0.98);
}

.popover-right-leave-to {
  opacity: 0;
  transform: translateX(-4px) scale(0.98);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* 确保 popover 不被遮挡 */
.popover {
  z-index: 9999 !important;
}
</style>