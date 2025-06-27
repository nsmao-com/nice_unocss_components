<template>
  <div class="relative w-full bg-white rounded-xl overflow-hidden shadow-sm border border-slate-200">
    <!-- Main carousel container -->
    <div 
      class="relative h-64 overflow-hidden"
      @mouseenter="handleMouseEnter"
      @mouseleave="handleMouseLeave"
    >
      <!-- Slides -->
      <div 
        class="flex transition-transform duration-500 ease-in-out h-full"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
      >
        <div
          v-for="(item, index) in items"
          :key="index"
          class="w-full h-full flex-shrink-0 relative flex items-center justify-center bg-gradient-to-br"
          :class="getSlideClass(index)"
        >
          <!-- Image content -->
          <div v-if="item.image" class="w-full h-full">
            <img 
              :src="item.image" 
              :alt="item.title || `Slide ${index + 1}`"
              class="w-full h-full object-cover"
            />
          </div>
          
          <!-- Text content overlay -->
          <div v-if="item.title || item.description" class="absolute inset-0 bg-black/20 flex items-center justify-center">
            <div class="text-center text-white px-6">
              <h3 v-if="item.title" class="text-2xl font-bold mb-2">{{ item.title }}</h3>
              <p v-if="item.description" class="text-lg opacity-90">{{ item.description }}</p>
            </div>
          </div>
          
          <!-- Default content for demo -->
          <div v-if="!item.image && !item.title" class="text-center">
            <div class="w-16 h-16 bg-white/20 rounded-full flex items-center justify-center mb-4 mx-auto">
              <span class="text-2xl font-bold text-white">{{ index + 1 }}</span>
            </div>
            <h3 class="text-xl font-semibold text-white mb-2">幻灯片 {{ index + 1 }}</h3>
            <p class="text-white/80">这是第 {{ index + 1 }} 张幻灯片的内容</p>
          </div>
        </div>
      </div>
      
      <!-- Navigation arrows -->
      <button
        v-if="showArrows"
        @click="prevSlide"
        class="absolute left-4 top-1/2 transform -translate-y-1/2 w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition-all duration-200 shadow-lg hover:shadow-xl z-10"
      >
        <ChevronLeft :size="20" class="text-slate-700" />
      </button>
      
      <button
        v-if="showArrows"
        @click="nextSlide"
        class="absolute right-4 top-1/2 transform -translate-y-1/2 w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition-all duration-200 shadow-lg hover:shadow-xl z-10"
      >
        <ChevronRight :size="20" class="text-slate-700" />
      </button>
      
      <!-- Indicators - moved inside the image area -->
      <div v-if="showIndicators" class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex items-center space-x-2 z-10">
        <button
          v-for="(item, index) in items"
          :key="`indicator-${index}`"
          @click="goToSlide(index)"
          class="w-2.5 h-2.5 rounded-full transition-all duration-300 ease-in-out backdrop-blur-sm"
          :class="{
            'bg-white scale-125 shadow-lg': currentIndex === index,
            'bg-white/60 hover:bg-white/80': currentIndex !== index
          }"
        ></button>
      </div>
      
      <!-- Play/Pause button -->
      <button
        v-if="showPlayPause"
        @click="toggleAutoplay"
        class="absolute top-4 right-4 w-8 h-8 bg-black/50 hover:bg-black/70 text-white rounded-full flex items-center justify-center transition-all duration-200 z-10"
      >
        <Play v-if="!isPlaying" :size="14" class="ml-0.5" />
        <Pause v-else :size="14" />
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue';
import { ChevronLeft, ChevronRight, Play, Pause } from 'lucide-vue-next';

const props = defineProps({
  items: {
    type: Array,
    required: true,
    default: () => []
  },
  autoplay: {
    type: Boolean,
    default: true
  },
  autoplayStart: {
    type: Boolean,
    default: true
  },
  interval: {
    type: Number,
    default: 3000
  },
  pauseOnHover: {
    type: Boolean,
    default: true
  },
  showArrows: {
    type: Boolean,
    default: true
  },
  showIndicators: {
    type: Boolean,
    default: true
  },
  showPlayPause: {
    type: Boolean,
    default: true
  }
});

const emit = defineEmits(['change']);

const currentIndex = ref(0);
const isPlaying = ref(props.autoplay && props.autoplayStart);
const isHovered = ref(false);
let autoplayTimer = null;

// Predefined gradient classes for demo slides
const gradientClasses = [
  'from-blue-500 to-purple-600',
  'from-green-500 to-blue-500', 
  'from-purple-500 to-pink-500',
  'from-yellow-500 to-red-500',
  'from-indigo-500 to-blue-600'
];

const getSlideClass = (index) => {
  return gradientClasses[index % gradientClasses.length];
};

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % props.items.length;
  emit('change', currentIndex.value);
};

const prevSlide = () => {
  currentIndex.value = currentIndex.value === 0 
    ? props.items.length - 1 
    : currentIndex.value - 1;
  emit('change', currentIndex.value);
};

const goToSlide = (index) => {
  currentIndex.value = index;
  emit('change', currentIndex.value);
};

const startAutoplay = () => {
  if (isPlaying.value && props.autoplay && props.items.length > 1) {
    // 如果pauseOnHover为true且鼠标悬停，则不启动
    if (props.pauseOnHover && isHovered.value) {
      return;
    }
    autoplayTimer = setInterval(nextSlide, props.interval);
  }
};

const stopAutoplay = () => {
  if (autoplayTimer) {
    clearInterval(autoplayTimer);
    autoplayTimer = null;
  }
};

const handleMouseEnter = () => {
  isHovered.value = true;
  if (props.pauseOnHover) {
    stopAutoplay();
  }
};

const handleMouseLeave = () => {
  isHovered.value = false;
  if (props.pauseOnHover && isPlaying.value) {
    startAutoplay();
  }
};

const toggleAutoplay = () => {
  isPlaying.value = !isPlaying.value;
  if (isPlaying.value) {
    startAutoplay();
  } else {
    stopAutoplay();
  }
};

// Watch for items changes
watch(() => props.items, () => {
  if (currentIndex.value >= props.items.length) {
    currentIndex.value = 0;
  }
});

// Watch for autoplay changes
watch(() => props.autoplay, (newVal) => {
  if (newVal && props.autoplayStart) {
    isPlaying.value = true;
    startAutoplay();
  } else {
    isPlaying.value = false;
    stopAutoplay();
  }
});

// Watch for playing state changes
watch(isPlaying, (newVal) => {
  if (newVal) {
    startAutoplay();
  } else {
    stopAutoplay();
  }
});

onMounted(() => {
  if (props.autoplay && props.autoplayStart && props.items.length > 1) {
    isPlaying.value = true;
    startAutoplay();
  }
});

onUnmounted(() => {
  stopAutoplay();
});
</script> 