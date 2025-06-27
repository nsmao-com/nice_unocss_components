<template>
  <div :class="wrapperClass">
    <div :class="containerClass">
      <div :class="trackClass" ref="tabsContainer">
        <div
          v-for="(tab, index) in tabs"
          :key="index"
          :class="[tabItemClass, { 'text-slate-900 font-semibold': modelValue === index }]"
          @click="selectTab(index)"
          ref="tabItems"
        >
          {{ typeof tab === 'string' ? tab : tab.title }}
        </div>
        <div
          :class="sliderClass"
          :style="sliderStyle"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch, nextTick } from 'vue';

const props = defineProps({
  tabs: {
    type: Array,
    required: true,
  },
  modelValue: {
    type: Number,
    required: true,
  },
  vertical: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:modelValue']);

const tabsContainer = ref(null);
const tabItems = ref([]);
const sliderWidth = ref(0);
const sliderHeight = ref(0);
const sliderLeft = ref(0);
const sliderTop = ref(0);

// Dynamic classes based on orientation
const wrapperClass = computed(() => 
  props.vertical 
    ? 'h-full flex items-center justify-center px-4'
    : 'w-full flex justify-center py-4'
);

const containerClass = computed(() => 'bg-slate-100 rounded-lg p-1 shadow-sm');

const trackClass = computed(() => 
  props.vertical 
    ? 'relative flex flex-col'
    : 'relative flex'
);

const tabItemClass = computed(() => 
  props.vertical 
    ? 'relative px-5 py-2.5 cursor-pointer font-medium text-sm text-slate-500 rounded-md transition-all duration-200 z-2 whitespace-nowrap select-none hover:text-slate-600 text-center min-w-24 mb-1 last:mb-0'
    : 'relative px-5 py-2.5 cursor-pointer font-medium text-sm text-slate-500 rounded-md transition-all duration-200 z-2 whitespace-nowrap select-none hover:text-slate-600 mr-1 last:mr-0'
);

const sliderClass = computed(() => 
  'absolute bg-white rounded-md transition-all duration-250 z-1 shadow-sm'
);

const sliderStyle = computed(() => {
  if (props.vertical) {
    return {
      height: `${sliderHeight.value}px`,
      transform: `translateY(${sliderTop.value}px)`,
      left: '0px',
      right: '0px',
    };
  } else {
    return {
      width: `${sliderWidth.value}px`,
      transform: `translateX(${sliderLeft.value}px)`,
      top: '0px',
      bottom: '0px',
    };
  }
});

const selectTab = (index) => {
  emit('update:modelValue', index);
};

const updateSlider = () => {
  if (tabItems.value && tabItems.value[props.modelValue]) {
    const activeTab = tabItems.value[props.modelValue];
    const gapSize = 4; // gap-1 = 4px
    
    if (props.vertical) {
      sliderHeight.value = activeTab.offsetHeight;
      sliderTop.value = activeTab.offsetTop;
    } else {
      sliderWidth.value = activeTab.offsetWidth;
      sliderLeft.value = activeTab.offsetLeft;
    }
  }
};

onMounted(() => {
  nextTick(updateSlider);
});

watch(() => props.modelValue, () => {
  nextTick(updateSlider);
});

watch(() => props.tabs, () => {
  nextTick(updateSlider);
}, { deep: true });

watch(() => props.vertical, () => {
  nextTick(updateSlider);
});
</script>

<style scoped>
/* 响应式设计 */
@media (max-width: 640px) {
  .z-1 { z-index: 1; }
  .z-2 { z-index: 2; }
}
</style>

