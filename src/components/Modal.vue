<template>
  <Teleport to="body">
    <Transition
      name="modal"
      enter-active-class="duration-300 ease-out"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="duration-200 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="visible"
        class="fixed inset-0 z-50 flex items-center justify-center p-4"
        @click="handleBackdropClick"
      >
        <!-- 背景遮罩 -->
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm"></div>
        
        <!-- Modal内容 -->
        <Transition
          name="modal-content"
          enter-active-class="duration-300 ease-out"
          enter-from-class="scale-95 opacity-0 translate-y-4"
          enter-to-class="scale-100 opacity-100 translate-y-0"
          leave-active-class="duration-200 ease-in"
          leave-from-class="scale-100 opacity-100 translate-y-0"
          leave-to-class="scale-95 opacity-0 translate-y-4"
        >
          <div
            v-if="visible"
            :class="modalClass"
            @click.stop
          >
            <!-- Header -->
            <div class="flex items-center justify-between p-6">
              <h3 class="text-lg font-semibold text-slate-900">
                <slot name="title">{{ title }}</slot>
              </h3>
              <RippleButton
                @click="handleClose"
                size="sm"
                variant="ghost"
              >
                <template #icon>
                  <X :size="20" />
                </template>
              </RippleButton>
            </div>
            
            <!-- Body -->
            <div :class="bodyClass">
              <slot>
                <p class="text-slate-600">{{ content }}</p>
              </slot>
            </div>
            
            <!-- Footer -->
            <div v-if="showFooter" class="flex justify-end space-x-3 p-6">
              <slot name="footer" :close="handleClose" :confirm="handleConfirm">
                <RippleButton
                  v-if="showCancelButton"
                  :text="cancelText"
                  variant="ghost"
                  @click="handleClose"
                />
                <RippleButton
                  v-if="showConfirmButton"
                  :text="confirmText"
                  :variant="confirmVariant"
                  @click="handleConfirm"
                />
              </slot>
            </div>
          </div>
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { computed, watch, nextTick } from 'vue';
import { X } from 'lucide-vue-next';
import RippleButton from './RippleButton.vue';

const props = defineProps({
  // 显示状态
  visible: {
    type: Boolean,
    default: false,
  },
  // 标题
  title: {
    type: String,
    default: 'Modal Title',
  },
  // 内容
  content: {
    type: String,
    default: '',
  },
  // 尺寸
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg', 'xl', 'full'].includes(value),
  },
  // 是否显示footer
  showFooter: {
    type: Boolean,
    default: true,
  },
  // 是否显示取消按钮
  showCancelButton: {
    type: Boolean,
    default: true,
  },
  // 是否显示确认按钮
  showConfirmButton: {
    type: Boolean,
    default: true,
  },
  // 取消按钮文本
  cancelText: {
    type: String,
    default: 'Close',
  },
  // 确认按钮文本
  confirmText: {
    type: String,
    default: 'Action',
  },
  // 确认按钮变体
  confirmVariant: {
    type: String,
    default: 'primary',
  },
  // 是否可以点击背景关闭
  closeOnBackdrop: {
    type: Boolean,
    default: true,
  },
  // 是否可以按ESC关闭
  closeOnEsc: {
    type: Boolean,
    default: true,
  },
});

const emit = defineEmits(['update:visible', 'close', 'confirm']);

// Modal容器样式
const modalClass = computed(() => {
  const baseClasses = [
    'relative bg-white rounded-xl shadow-2xl',
    'max-h-[90vh] overflow-hidden flex flex-col',
  ];

  // 尺寸样式
  const sizeClasses = {
    sm: 'w-full max-w-md',
    md: 'w-full max-w-lg',
    lg: 'w-full max-w-2xl',
    xl: 'w-full max-w-4xl',
    full: 'w-[95vw] h-[95vh]',
  };

  return [
    ...baseClasses,
    sizeClasses[props.size],
  ].join(' ');
});

// Body样式
const bodyClass = computed(() => {
  const baseClasses = [
    'flex-1 overflow-y-auto',
  ];

  if (props.showFooter) {
    baseClasses.push('p-6');
  } else {
    baseClasses.push('p-6 pb-6');
  }

  return baseClasses.join(' ');
});

// 处理关闭
const handleClose = () => {
  emit('update:visible', false);
  emit('close');
};

// 处理确认
const handleConfirm = () => {
  emit('confirm');
  // 注意：不自动关闭，由父组件决定
};

// 处理背景点击
const handleBackdropClick = () => {
  if (props.closeOnBackdrop) {
    handleClose();
  }
};

// 处理ESC键
const handleEscKey = (event) => {
  if (event.key === 'Escape' && props.closeOnEsc && props.visible) {
    handleClose();
  }
};

// 监听键盘事件
watch(() => props.visible, (newVisible) => {
  if (newVisible) {
    nextTick(() => {
      document.addEventListener('keydown', handleEscKey);
      document.body.style.overflow = 'hidden';
    });
  } else {
    document.removeEventListener('keydown', handleEscKey);
    document.body.style.overflow = '';
  }
});

// 组件卸载时清理
import { onUnmounted } from 'vue';
onUnmounted(() => {
  document.removeEventListener('keydown', handleEscKey);
  document.body.style.overflow = '';
});
</script>

<style scoped>
/* Modal动画 */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.3s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-content-enter-active,
.modal-content-leave-active {
  transition: all 0.3s ease;
}

.modal-content-enter-from,
.modal-content-leave-to {
  opacity: 0;
  transform: scale(0.95);
}
</style> 