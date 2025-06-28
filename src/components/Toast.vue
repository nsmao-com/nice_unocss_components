<template>
  <Teleport to="body">
    <Transition :name="transitionName" appear>
      <div
        v-if="visible"
        :class="toastContainerClass"
        :style="toastContainerStyle"
        @click="handleClick"
        data-toast="true"
        :data-position="position"
        :data-animation="animation"
      >
        <div :class="toastClass">
          <!-- 图标 -->
          <div v-if="showIcon" :class="iconClass">
            <component v-if="currentIcon" :is="currentIcon" :size="iconSize" />
          </div>
          
          <!-- 内容区域 -->
          <div class="flex-1 min-w-0">
            <div v-if="title" :class="titleClass">{{ title }}</div>
            <div :class="messageClass">
              <slot>{{ message }}</slot>
            </div>
          </div>
          
          <!-- 关闭按钮 -->
          <button
            v-if="closable"
            @click.stop="handleClose"
            :class="closeButtonClass"
          >
            <X :size="closeIconSize" />
          </button>
          
          <!-- 进度条 -->
          <div v-if="showProgress && duration > 0" :class="progressBarClass">
            <div 
              :class="progressFillClass"
              :style="progressStyle"
            ></div>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { computed, ref, watch, onUnmounted } from 'vue';
import { X, CheckCircle, AlertCircle, AlertTriangle, Info, Bell } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  visible: { type: Boolean, default: false },
  title: { type: String, default: '' },
  message: { type: String, default: '' },

  // 样式
  variant: { type: String, default: 'default' }, // default, success, warning, error, info
  position: { type: String, default: 'top-right' }, // top-left, top-right, bottom-left, bottom-right
  size: { type: String, default: 'md' }, // sm, md, lg
  offset: { type: Number, default: 0 }, // 垂直偏移量，用于堆叠多个 Toast

  // 功能
  duration: { type: Number, default: 4000 }, // 0 表示不自动关闭
  closable: { type: Boolean, default: true },
  clickToClose: { type: Boolean, default: false },
  showProgress: { type: Boolean, default: true },

  // 图标
  icon: { type: [String, Object, Function], default: null },
  showIcon: { type: Boolean, default: true },
  iconSize: { type: Number, default: 20 },

  // 动画
  animation: { type: String, default: 'slide' }, // slide, fade, bounce
});

const emit = defineEmits(['update:visible', 'close', 'click']);

// 状态
const progress = ref(100);
let timer = null;
let progressTimer = null;

// 默认图标映射
const defaultIcons = {
  default: Bell,
  success: CheckCircle,
  warning: AlertTriangle,
  error: AlertCircle,
  info: Info,
};

// 当前图标
const currentIcon = computed(() => {
  if (!props.showIcon) return null;
  return props.icon || defaultIcons[props.variant] || defaultIcons.default;
});

// Toast容器样式
const toastContainerClass = computed(() => {
  const baseClasses = ['fixed z-50 pointer-events-auto'];

  // 位置和偏移
  switch (props.position) {
    case 'top-left':
      baseClasses.push('left-4');
      break;
    case 'top-right':
      baseClasses.push('right-4');
      break;
    case 'bottom-left':
      baseClasses.push('left-4');
      break;
    case 'bottom-right':
      baseClasses.push('right-4');
      break;
  }

  return baseClasses;
});

// 动态计算位置样式
const toastContainerStyle = computed(() => {
  const isTop = props.position.includes('top');
  const baseOffset = 16; // 1rem = 16px
  const totalOffset = baseOffset + props.offset;

  return {
    [isTop ? 'top' : 'bottom']: `${totalOffset}px`
  };
});

// Toast主体样式
const toastClass = computed(() => {
  const baseClasses = [
    'relative flex items-start p-4 rounded-lg shadow-lg border backdrop-blur-sm',
    'max-w-sm w-full transition-all duration-200 cursor-default',
    'overflow-hidden'
  ];
  
  // 尺寸
  switch (props.size) {
    case 'sm':
      baseClasses.push('p-3 text-sm max-w-xs');
      break;
    case 'lg':
      baseClasses.push('p-5 text-base max-w-md');
      break;
    default:
      baseClasses.push('p-4 text-sm max-w-sm');
  }
  
  // 变体样式
  switch (props.variant) {
    case 'success':
      baseClasses.push('bg-green-50/95 border-green-200 text-green-800');
      break;
    case 'warning':
      baseClasses.push('bg-yellow-50/95 border-yellow-200 text-yellow-800');
      break;
    case 'error':
      baseClasses.push('bg-red-50/95 border-red-200 text-red-800');
      break;
    case 'info':
      baseClasses.push('bg-blue-50/95 border-blue-200 text-blue-800');
      break;
    default:
      baseClasses.push('bg-white/95 border-slate-200 text-slate-800');
  }
  
  // 点击关闭样式
  if (props.clickToClose) {
    baseClasses.push('cursor-pointer hover:shadow-xl');
  }
  
  return baseClasses;
});

// 图标样式
const iconClass = computed(() => {
  const baseClasses = ['flex-shrink-0 mr-3'];
  
  // 图标颜色
  switch (props.variant) {
    case 'success':
      baseClasses.push('text-green-600');
      break;
    case 'warning':
      baseClasses.push('text-yellow-600');
      break;
    case 'error':
      baseClasses.push('text-red-600');
      break;
    case 'info':
      baseClasses.push('text-blue-600');
      break;
    default:
      baseClasses.push('text-slate-600');
  }
  
  return baseClasses;
});

// 标题样式
const titleClass = computed(() => {
  const baseClasses = ['font-semibold mb-1'];
  
  switch (props.size) {
    case 'sm':
      baseClasses.push('text-sm');
      break;
    case 'lg':
      baseClasses.push('text-base');
      break;
    default:
      baseClasses.push('text-sm');
  }
  
  return baseClasses;
});

// 消息样式
const messageClass = computed(() => {
  const baseClasses = ['leading-relaxed'];
  
  switch (props.size) {
    case 'sm':
      baseClasses.push('text-xs');
      break;
    case 'lg':
      baseClasses.push('text-sm');
      break;
    default:
      baseClasses.push('text-xs');
  }
  
  return baseClasses;
});

// 关闭按钮样式
const closeButtonClass = computed(() => {
  let sizeClasses = 'w-6 h-6';

  // 根据 Toast 尺寸调整按钮大小
  switch (props.size) {
    case 'sm':
      sizeClasses = 'w-5 h-5';
      break;
    case 'lg':
      sizeClasses = 'w-7 h-7';
      break;
    default:
      sizeClasses = 'w-6 h-6';
  }

  const baseClasses = [
    'flex-shrink-0 ml-3 flex items-center justify-center rounded-md transition-colors duration-200',
    'hover:bg-black/10 focus:outline-none focus:ring-2 focus:ring-offset-2',
    sizeClasses
  ];
  
  // 关闭按钮颜色
  switch (props.variant) {
    case 'success':
      baseClasses.push('text-green-600 hover:text-green-700 focus:ring-green-500');
      break;
    case 'warning':
      baseClasses.push('text-yellow-600 hover:text-yellow-700 focus:ring-yellow-500');
      break;
    case 'error':
      baseClasses.push('text-red-600 hover:text-red-700 focus:ring-red-500');
      break;
    case 'info':
      baseClasses.push('text-blue-600 hover:text-blue-700 focus:ring-blue-500');
      break;
    default:
      baseClasses.push('text-slate-600 hover:text-slate-700 focus:ring-slate-500');
  }
  
  return baseClasses;
});

// 关闭按钮图标尺寸
const closeIconSize = computed(() => {
  switch (props.size) {
    case 'sm':
      return 12;
    case 'lg':
      return 18;
    default:
      return 14;
  }
});

// 进度条样式
const progressBarClass = computed(() => [
  'absolute bottom-0 left-0 right-0 h-1 bg-black/10'
]);

const progressFillClass = computed(() => {
  const baseClasses = ['h-full transition-all duration-100 ease-linear'];
  
  // 进度条颜色
  switch (props.variant) {
    case 'success':
      baseClasses.push('bg-green-600');
      break;
    case 'warning':
      baseClasses.push('bg-yellow-600');
      break;
    case 'error':
      baseClasses.push('bg-red-600');
      break;
    case 'info':
      baseClasses.push('bg-blue-600');
      break;
    default:
      baseClasses.push('bg-slate-600');
  }
  
  return baseClasses;
});

// 进度条样式
const progressStyle = computed(() => ({
  width: `${progress.value}%`
}));

// 过渡动画名称
const transitionName = computed(() => {
  switch (props.animation) {
    case 'fade':
      return 'toast-fade';
    case 'bounce':
      return 'toast-bounce';
    case 'slide':
    default:
      // 根据位置决定滑动方向
      if (props.position.includes('left')) {
        return 'toast-slide-left';
      } else {
        return 'toast-slide';
      }
  }
});

// 事件处理
const handleClose = () => {
  clearTimers();
  emit('update:visible', false);
  emit('close');
};

const handleClick = () => {
  emit('click');
  if (props.clickToClose) {
    handleClose();
  }
};

// 定时器管理
const clearTimers = () => {
  if (timer) {
    clearTimeout(timer);
    timer = null;
  }
  if (progressTimer) {
    clearInterval(progressTimer);
    progressTimer = null;
  }
};

const startTimer = () => {
  if (props.duration > 0) {
    progress.value = 100;
    
    // 进度条动画
    if (props.showProgress) {
      const interval = 50; // 50ms 更新一次
      const step = (interval / props.duration) * 100;
      
      progressTimer = setInterval(() => {
        progress.value -= step;
        if (progress.value <= 0) {
          progress.value = 0;
          clearInterval(progressTimer);
        }
      }, interval);
    }
    
    // 自动关闭
    timer = setTimeout(() => {
      handleClose();
    }, props.duration);
  }
};

// 监听 visible 变化
watch(() => props.visible, (newVisible) => {
  if (newVisible) {
    startTimer();
  } else {
    clearTimers();
  }
}, { immediate: true });



// 组件卸载时清理定时器
onUnmounted(() => {
  clearTimers();
});
</script>

<style scoped>
/* 滑动动画 */
.toast-slide-enter-active,
.toast-slide-leave-active {
  transition: all 0.3s ease-out;
}

.toast-slide-enter-from {
  transform: translateX(100%);
  opacity: 0;
}

.toast-slide-leave-to {
  transform: translateX(100%);
  opacity: 0;
}

/* 左侧滑动动画 */
.toast-slide-left-enter-active,
.toast-slide-left-leave-active {
  transition: all 0.3s ease-out;
}

.toast-slide-left-enter-from {
  transform: translateX(-100%);
  opacity: 0;
}

.toast-slide-left-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}

/* 淡入淡出动画 */
.toast-fade-enter-active,
.toast-fade-leave-active {
  transition: opacity 0.3s ease-out;
}

.toast-fade-enter-from,
.toast-fade-leave-to {
  opacity: 0;
}

/* 弹跳动画 */
.toast-bounce-enter-active {
  animation: toast-bounce-in 0.5s ease-out;
}

.toast-bounce-leave-active {
  animation: toast-bounce-out 0.3s ease-in;
}

@keyframes toast-bounce-in {
  0% {
    transform: scale(0.3) translateY(-50px);
    opacity: 0;
  }
  50% {
    transform: scale(1.05);
  }
  70% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
}

@keyframes toast-bounce-out {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  100% {
    transform: scale(0.3) translateY(-50px);
    opacity: 0;
  }
}


</style> 