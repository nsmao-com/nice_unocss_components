<template>
  <div 
    class="relative inline-block text-left" 
    ref="dropdownRef"
    @mouseenter="handleMouseEnter"
    @mouseleave="handleMouseLeave"
  >
    <!-- 触发按钮 -->
    <button
      @click="handleButtonClick"
      :class="triggerClass"
      :disabled="disabled"
      type="button"
      aria-haspopup="true"
      :aria-expanded="isOpen"
    >
      <span class="flex items-center">
        <!-- 前置图标 -->
        <svg v-if="prefixIcon" :class="prefixIconClass" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <g v-html="prefixIcon"></g>
        </svg>
        
        <!-- 文字内容 -->
        <span>{{ triggerText }}</span>
        
        <!-- 下拉箭头 -->
        <svg 
          :class="arrowClass"
          viewBox="0 0 24 24" 
          fill="none" 
          xmlns="http://www.w3.org/2000/svg"
        >
          <path d="M6 9l6 6 6-6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </span>
    </button>

    <!-- 下拉菜单 -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform scale-95 opacity-0"
      enter-to-class="transform scale-100 opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="transform scale-100 opacity-100"
      leave-to-class="transform scale-95 opacity-0"
    >
      <div
        v-if="isOpen"
        :class="dropdownMenuClass"
        role="menu"
        aria-orientation="vertical"
      >
        <div class="p-2" role="none">
          <template v-for="(item, index) in items" :key="index">
            <!-- 分割线 -->
            <div 
              v-if="item.divider" 
              class="border-t border-gray-100 my-1"
              role="separator"
            ></div>
            
            <!-- 菜单项 -->
            <button
              v-else
              @click="handleItemClick(item)"
              :class="getItemClass(item)"
              :disabled="item.disabled"
              role="menuitem"
              type="button"
            >
              <!-- 项目图标 -->
              <svg v-if="item.icon" class="w-4 h-4 mr-3" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g v-html="item.icon"></g>
              </svg>
              
              <!-- 项目文字 -->
              <span class="flex-1 text-left">{{ item.label }}</span>
              
              <!-- 右侧内容（快捷键等） -->
              <span v-if="item.shortcut" class="text-xs text-gray-400 ml-2">{{ item.shortcut }}</span>
            </button>
          </template>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  // 基础属性
  triggerText: { type: String, default: 'Open Menu' },
  items: { type: Array, required: true },
  
  // 触发器样式
  variant: { type: String, default: 'default' }, // default, primary, outline, ghost
  size: { type: String, default: 'md' }, // sm, md, lg
  disabled: { type: Boolean, default: false },
  rounded: { type: Boolean, default: false }, // false: 微微圆角, true: 椭圆形
  
  // 触发模式
  trigger: { type: String, default: 'click' }, // click, hover
  
  // 图标
  prefixIcon: { type: String, default: null },
  
  // 下拉菜单位置
  placement: { type: String, default: 'bottom-start' }, // bottom-start, bottom-end, top-start, top-end
  
  // 其他选项
  closeOnClick: { type: Boolean, default: true },
  autoClose: { type: Boolean, default: true },
  hoverDelay: { type: Number, default: 150 }, // hover模式的延迟时间（毫秒）
});

const emit = defineEmits(['select', 'open', 'close']);

// 状态
const isOpen = ref(false);
const dropdownRef = ref(null);
let hoverTimer = null;

// 处理按钮点击
const handleButtonClick = () => {
  if (props.disabled) return;
  
  // 只有在点击模式下才响应点击事件
  if (props.trigger === 'click') {
    toggleDropdown();
  }
};

// 切换下拉菜单
const toggleDropdown = () => {
  if (props.disabled) return;
  
  if (isOpen.value) {
    closeDropdown();
  } else {
    openDropdown();
  }
};

// Hover模式的延迟打开
const handleMouseEnter = () => {
  if (props.disabled || props.trigger !== 'hover') return;
  
  clearTimeout(hoverTimer);
  hoverTimer = setTimeout(() => {
    openDropdown();
  }, props.hoverDelay);
};

// Hover模式的延迟关闭
const handleMouseLeave = () => {
  if (props.disabled || props.trigger !== 'hover') return;
  
  clearTimeout(hoverTimer);
  hoverTimer = setTimeout(() => {
    closeDropdown();
  }, props.hoverDelay);
};

// 打开下拉菜单
const openDropdown = () => {
  isOpen.value = true;
  emit('open');
};

// 关闭下拉菜单
const closeDropdown = () => {
  isOpen.value = false;
  emit('close');
};

// 处理项目点击
const handleItemClick = (item) => {
  if (item.disabled) return;
  
  emit('select', item);
  
  if (props.closeOnClick) {
    closeDropdown();
  }
};

// 触发按钮样式
const triggerClass = computed(() => {
  const baseClasses = [
    'inline-flex items-center justify-center font-medium transition-colors duration-200 cursor-pointer',
  ];

  // 尺寸和圆角
  const roundedClass = props.rounded ? 'rounded-3xl' : 'rounded-lg';
  
  switch (props.size) {
    case 'sm':
      baseClasses.push(`px-3 py-1.5 text-sm ${roundedClass} gap-2`);
      break;
    case 'md':
      baseClasses.push(`px-4 py-2 text-sm ${roundedClass} gap-2`);
      break;
    case 'lg':
      baseClasses.push(`px-6 py-3 text-base ${roundedClass} gap-3`);
      break;
  }

  // 变体样式
  if (props.disabled) {
    baseClasses.push('opacity-50 cursor-not-allowed bg-gray-100 cursor-pointer text-gray-400');
  } else {
    switch (props.variant) {
      case 'default':
        baseClasses.push(
          'bg-white border border-gray-300 text-gray-700',
          'hover:bg-gray-50'
        );
        break;
      case 'primary':
        baseClasses.push(
          'bg-blue-600 text-white border border-blue-600',
          'hover:bg-blue-700'
        );
        break;
      case 'outline':
        baseClasses.push(
          'bg-transparent border border-gray-300 text-gray-700',
          'hover:bg-gray-50'
        );
        break;
      case 'ghost':
        baseClasses.push(
          'bg-transparent text-gray-700',
          'hover:bg-gray-100'
        );
        break;
    }
  }

  return baseClasses;
});

// 前置图标样式
const prefixIconClass = computed(() => {
  const classes = ['mr-2'];
  
  switch (props.size) {
    case 'sm': classes.push('w-4 h-4'); break;
    case 'md': classes.push('w-4 h-4'); break;
    case 'lg': classes.push('w-5 h-5'); break;
  }

  return classes;
});

// 箭头样式
const arrowClass = computed(() => {
  const classes = [
    'ml-2 transition-transform duration-200',
    isOpen.value ? 'transform rotate-180' : '',
  ];
  
  switch (props.size) {
    case 'sm': classes.push('w-3 h-3'); break;
    case 'md': classes.push('w-4 h-4'); break;
    case 'lg': classes.push('w-4 h-4'); break;
  }

  return classes;
});

// 下拉菜单样式
const dropdownMenuClass = computed(() => {
  const menuRoundedClass = 'rounded-xl';
  const baseClasses = [
    `absolute z-50 mt-1 bg-white ${menuRoundedClass} shadow-lg border border-gray-200`,
    'min-w-48 max-w-xs',
  ];

  // 位置
  switch (props.placement) {
    case 'bottom-start':
      baseClasses.push('left-0');
      break;
    case 'bottom-end':
      baseClasses.push('right-0');
      break;
    case 'top-start':
      baseClasses.push('bottom-full mb-1 left-0');
      break;
    case 'top-end':
      baseClasses.push('bottom-full mb-1 right-0');
      break;
  }

  return baseClasses;
});

// 获取菜单项样式
const getItemClass = (item) => {
  const baseClasses = [
    'w-full px-3 py-2 text-sm text-left flex items-center rounded-lg',
    'transition-colors duration-150',
  ];

  if (item.disabled) {
    baseClasses.push('text-gray-400 cursor-not-allowed bg-white');
  } else if (item.variant === 'danger') {
    baseClasses.push('text-red-600 bg-white hover:bg-gray-100 hover:text-red-700');
  } else {
    baseClasses.push('text-gray-700 bg-white hover:bg-gray-100 hover:text-gray-900');
  }

  return baseClasses;
};

// 点击外部关闭
const handleClickOutside = (event) => {
  if (props.autoClose && dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    // 清除hover定时器，避免点击外部关闭后被hover重新打开
    clearTimeout(hoverTimer);
    closeDropdown();
  }
};

// ESC键关闭
const handleEscapeKey = (event) => {
  if (event.key === 'Escape' && isOpen.value) {
    closeDropdown();
  }
};

onMounted(() => {
  document.addEventListener('click', handleClickOutside);
  document.addEventListener('keydown', handleEscapeKey);
});

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside);
  document.removeEventListener('keydown', handleEscapeKey);
  clearTimeout(hoverTimer);
});
</script> 