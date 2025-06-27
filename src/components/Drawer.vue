<template>
  <Teleport to="body">
    <Transition
      name="drawer-overlay"
      enter-active-class="duration-300"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="duration-200"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="visible || isAnimating"
        :class="containerClass"
        @click="handleBackdropClick"
      >
        <!-- 背景遮罩 -->
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm"></div>
        
        <!-- 抽屉内容 -->
        <div
          :class="drawerClass"
          :style="drawerStyle"
          @click.stop
        >
          <!-- Header -->
          <div v-if="showHeader" :class="headerClass">
            <h3 class="text-lg font-semibold text-slate-900">
              <slot name="title">{{ title }}</slot>
            </h3>
                          <button
                v-if="closable"
                @click="handleClose"
                class="w-8 h-8 flex items-center justify-center text-slate-400 hover:text-slate-600 hover:bg-slate-100 active:bg-slate-200 transition-all duration-200 rounded-full shrink-0"
              >
                <X :size="16" />
              </button>
          </div>
          
          <!-- Body -->
          <div :class="bodyClass">
            <slot>
              <p class="text-slate-600">{{ content }}</p>
            </slot>
          </div>
          
          <!-- Footer -->
          <div v-if="showFooter" :class="footerClass">
            <slot name="footer" :close="handleClose">
              <div class="flex justify-end space-x-3">
                <button
                  v-if="showCancelButton"
                  @click="handleClose"
                  class="px-4 py-2 text-sm font-medium text-slate-700 bg-white border border-slate-300 rounded-lg hover:bg-slate-50 transition-colors"
                >
                  {{ cancelText }}
                </button>
                <button
                  v-if="showConfirmButton"
                  @click="handleConfirm"
                  :class="confirmButtonClass"
                >
                  {{ confirmText }}
                </button>
              </div>
            </slot>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { computed, watch, nextTick, onUnmounted, onMounted, ref } from 'vue';
import { X } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  visible: { type: Boolean, default: false },
  title: { type: String, default: 'Drawer Title' },
  content: { type: String, default: '' },
  
  // 抽屉位置和尺寸
  placement: { type: String, default: 'right' }, // left, right, top, bottom
  size: { type: String, default: 'md' }, // sm, md, lg, xl, full
  
  // 显示控制
  showHeader: { type: Boolean, default: true },
  showFooter: { type: Boolean, default: false },
  closable: { type: Boolean, default: true },
  
  // 按钮
  showCancelButton: { type: Boolean, default: true },
  showConfirmButton: { type: Boolean, default: false },
  cancelText: { type: String, default: 'Close' },
  confirmText: { type: String, default: 'Confirm' },
  confirmVariant: { type: String, default: 'primary' },
  
  // 行为
  closeOnBackdrop: { type: Boolean, default: true },
  closeOnEsc: { type: Boolean, default: true },
});

const emit = defineEmits(['update:visible', 'close', 'confirm']);

// 滑动状态
const isAnimating = ref(false);
const translateValue = ref('');

// 获取隐藏时的transform值
const getHideTransform = () => {
  switch (props.placement) {
    case 'left': return 'translateX(-100%)';
    case 'right': return 'translateX(100%)';
    case 'top': return 'translateY(-100%)';
    case 'bottom': return 'translateY(100%)';
    default: return 'translateX(100%)';
  }
};

// 初始化translate值
const initTranslateValue = () => {
  if (!props.visible) {
    translateValue.value = getHideTransform();
  } else {
    translateValue.value = 'translate(0, 0)';
  }
};

// 容器样式
const containerClass = computed(() => {
  const baseClasses = ['fixed inset-0 z-50'];
  
  switch (props.placement) {
    case 'left':
      baseClasses.push('flex justify-start items-stretch');
      break;
    case 'right':
      baseClasses.push('flex justify-end items-stretch');
      break;
    case 'top':
      baseClasses.push('flex flex-col justify-start items-stretch');
      break;
    case 'bottom':
      baseClasses.push('flex flex-col justify-end items-stretch');
      break;
  }
  
  return baseClasses;
});

// 抽屉主体样式
const drawerClass = computed(() => {
  const baseClasses = [
    'relative bg-white overflow-hidden flex flex-col',
  ];

  // 位置、圆角和特定阴影
  switch (props.placement) {
    case 'left':
      baseClasses.push('h-full rounded-r-xl drawer-left');
      break;
    case 'right':
      baseClasses.push('h-full rounded-l-xl drawer-right');
      break;
    case 'top':
      baseClasses.push('w-full rounded-b-xl drawer-top');
      break;
    case 'bottom':
      baseClasses.push('w-full rounded-t-xl drawer-bottom');
      break;
  }

  // 尺寸
  if (props.placement === 'left' || props.placement === 'right') {
    // 左右抽屉的宽度
    switch (props.size) {
      case 'sm': baseClasses.push('w-80'); break;
      case 'md': baseClasses.push('w-96'); break;
      case 'lg': baseClasses.push('w-[32rem]'); break;
      case 'xl': baseClasses.push('w-[40rem]'); break;
      case 'full': baseClasses.push('w-full'); break;
    }
  } else {
    // 上下抽屉的高度
    switch (props.size) {
      case 'sm': baseClasses.push('h-80'); break;
      case 'md': baseClasses.push('h-96'); break;
      case 'lg': baseClasses.push('h-[32rem]'); break;
      case 'xl': baseClasses.push('h-[40rem]'); break;
      case 'full': baseClasses.push('h-full'); break;
    }
  }

  return baseClasses;
});

// 抽屉动态样式
const drawerStyle = computed(() => {
  const baseStyle = {
    transform: translateValue.value || getHideTransform(),
    transition: isAnimating.value ? getTransition() : 'none'
  };
  
  return baseStyle;
});

// 获取过渡动画
const getTransition = () => {
  if (props.visible) {
    return 'transform 0.4s cubic-bezier(0.25, 0.1, 0.25, 1)';
  } else {
    return 'transform 0.25s cubic-bezier(0.4, 0, 0.2, 1)';
  }
};

// Header样式
const headerClass = computed(() => {
  const classes = ['flex items-center justify-between p-4 flex-shrink-0'];
  return classes;
});

// Body样式
const bodyClass = computed(() => {
  const classes = ['flex-1 p-4 overflow-y-auto'];
  return classes;
});

// Footer样式
const footerClass = computed(() => {
  const classes = ['flex-shrink-0 p-4 border-t border-slate-200 bg-slate-50'];
  return classes;
});

// 确认按钮样式
const confirmButtonClass = computed(() => {
  const baseClasses = ['px-4 py-2 text-sm font-medium rounded-lg transition-colors'];
  
  switch (props.confirmVariant) {
    case 'primary':
      baseClasses.push('text-white bg-blue-600 hover:bg-blue-700');
      break;
    case 'success':
      baseClasses.push('text-white bg-green-600 hover:bg-green-700');
      break;
    case 'warning':
      baseClasses.push('text-white bg-amber-600 hover:bg-amber-700');
      break;
    case 'danger':
      baseClasses.push('text-white bg-red-600 hover:bg-red-700');
      break;
    default:
      baseClasses.push('text-white bg-slate-600 hover:bg-slate-700');
      break;
  }
  
  return baseClasses;
});



// 事件处理
const handleClose = () => {
  emit('update:visible', false);
  emit('close');
};

const handleConfirm = () => {
  emit('confirm');
};

const handleBackdropClick = () => {
  if (props.closeOnBackdrop) handleClose();
};

// ESC键监听
const handleEscKey = (event) => {
  if (event.key === 'Escape' && props.closeOnEsc && props.visible) {
    handleClose();
  }
};

watch(() => props.visible, (newVisible) => {
  if (newVisible) {
    // 显示抽屉
    isAnimating.value = true;
    // 首先设置初始隐藏位置
    translateValue.value = getHideTransform();
    
    nextTick(() => {
      // 然后滑入到显示位置
      setTimeout(() => {
        translateValue.value = 'translate(0, 0)';
      }, 10);
      
      document.addEventListener('keydown', handleEscKey);
      document.body.style.overflow = 'hidden';
      
      // 动画结束后重置状态
      setTimeout(() => {
        isAnimating.value = false;
      }, 400);
    });
  } else {
    // 隐藏抽屉
    isAnimating.value = true;
    const hideTransform = getHideTransform();
    translateValue.value = hideTransform;
    
    document.removeEventListener('keydown', handleEscKey);
    document.body.style.overflow = '';
    
    // 动画结束后重置状态
    setTimeout(() => {
      isAnimating.value = false;
      translateValue.value = '';
    }, 250);
  }
});

// 组件挂载时初始化
onMounted(() => {
  initTranslateValue();
});

onUnmounted(() => {
  document.removeEventListener('keydown', handleEscKey);
  document.body.style.overflow = '';
});
</script>

<style scoped>
/* 背景遮罩动画 */
.drawer-overlay-enter-active {
  transition: opacity 0.3s ease;
}
.drawer-overlay-leave-active {
  transition: opacity 0.2s ease;
}
.drawer-overlay-enter-from, .drawer-overlay-leave-to {
  opacity: 0;
}

/* 优化动画性能 */
.drawer-left,
.drawer-right,
.drawer-top,
.drawer-bottom {
  will-change: transform;
  backface-visibility: hidden;
}

/* 为不同方向添加特定的阴影效果 */
.drawer-left {
  box-shadow: 4px 0 20px -2px rgba(0, 0, 0, 0.25);
}

.drawer-right {
  box-shadow: -4px 0 20px -2px rgba(0, 0, 0, 0.25);
}

.drawer-top {
  box-shadow: 0 4px 20px -2px rgba(0, 0, 0, 0.25);
}

.drawer-bottom {
  box-shadow: 0 -4px 20px -2px rgba(0, 0, 0, 0.25);
}
</style> 