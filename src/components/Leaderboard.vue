<template>
  <div :class="leaderboardClass">
    <!-- 标题栏 -->
    <div v-if="title" class="flex items-center justify-between mb-8">
      <div class="flex items-center space-x-3">
        <div 
          class="w-10 h-10 rounded-xl flex items-center justify-center"
          style="background: linear-gradient(to right, #facc15, #f97316);"
        >
          <svg class="w-5 h-5 text-white" fill="currentColor" viewBox="0 0 20 20">
            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
          </svg>
        </div>
        <div>
          <h3 class="text-2xl font-bold text-gray-900">{{ title }}</h3>
          <p class="text-sm text-gray-500">实时排行榜</p>
        </div>
      </div>
      <div v-if="showRefresh" class="flex items-center space-x-3">
        <div class="text-xs text-gray-500">
          {{ displayItems.length }} 位用户
        </div>
        <button 
          @click="handleRefresh"
          class="w-10 h-10 bg-white border border-gray-200 hover:border-gray-300 rounded-xl flex items-center justify-center transition-all duration-200 hover:shadow-md group"
          :disabled="loading"
        >
          <svg :class="['w-4 h-4 text-gray-600 group-hover:text-gray-900 transition-colors', { 'animate-spin': loading }]" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"></path>
          </svg>
        </button>
      </div>
    </div>

    <!-- 前三名特殊展示 -->
    <div v-if="displayItems.length >= 3" class="mb-8">
      <div class="grid grid-cols-3 gap-4 mb-6">
        <!-- 第二名 -->
        <div class="flex flex-col items-center pt-8" :style="animationStyle(1)">
          <div class="relative mb-4">
            <div class="w-16 h-16 rounded-2xl overflow-hidden border-4 border-gray-300 shadow-lg">
              <img 
                v-if="displayItems[1].avatar" 
                :src="displayItems[1].avatar" 
                :alt="displayItems[1].name"
                class="w-full h-full object-cover"
                @error="handleImageError"
              />
              <div 
                v-else 
                class="w-full h-full flex items-center justify-center text-white font-bold text-lg"
                style="background: linear-gradient(to bottom right, #9ca3af, #6b7280);"
              >
                {{ getInitials(displayItems[1].name) }}
              </div>
            </div>
            <div 
              class="absolute -top-2 -right-2 w-8 h-8 rounded-full flex items-center justify-center shadow-lg"
              style="background: linear-gradient(to bottom right, #d1d5db, #9ca3af);"
            >
              <span class="text-white font-bold text-sm">2</span>
            </div>
            <div v-if="showOnlineStatus && displayItems[1].online" class="absolute -bottom-1 -right-1 w-4 h-4 bg-green-500 border-2 border-white rounded-full"></div>
          </div>
          <h4 class="font-semibold text-gray-900 text-center mb-1">{{ displayItems[1].name }}</h4>
          <p v-if="displayItems[1].subtitle" class="text-xs text-gray-500 text-center mb-2">{{ displayItems[1].subtitle }}</p>
          <div class="bg-gray-100 rounded-lg px-3 py-1">
            <span class="text-sm font-bold text-gray-700">{{ formatScore(displayItems[1].score) }}</span>
            <span v-if="scoreUnit" class="text-xs text-gray-500 ml-1">{{ scoreUnit }}</span>
          </div>
        </div>

        <!-- 第一名 -->
        <div class="flex flex-col items-center" :style="animationStyle(0)">
          <div class="relative mb-4">
            <div class="w-20 h-20 rounded-2xl overflow-hidden border-4 border-yellow-400 shadow-xl">
              <img 
                v-if="displayItems[0].avatar" 
                :src="displayItems[0].avatar" 
                :alt="displayItems[0].name"
                class="w-full h-full object-cover"
                @error="handleImageError"
              />
              <div 
                v-else 
                class="w-full h-full flex items-center justify-center text-white font-bold text-xl"
                style="background: linear-gradient(to bottom right, #facc15, #f97316);"
              >
                {{ getInitials(displayItems[0].name) }}
              </div>
            </div>
            <div 
              class="absolute -top-3 -right-3 w-10 h-10 rounded-full flex items-center justify-center shadow-lg"
              style="background: linear-gradient(to bottom right, #facc15, #f97316);"
            >
              <svg class="w-5 h-5 text-white" fill="currentColor" viewBox="0 0 20 20">
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
              </svg>
            </div>
            <div v-if="showOnlineStatus && displayItems[0].online" class="absolute -bottom-1 -right-1 w-4 h-4 bg-green-500 border-2 border-white rounded-full"></div>
          </div>
          <h4 class="font-bold text-gray-900 text-center mb-1 text-lg">{{ displayItems[0].name }}</h4>
          <p v-if="displayItems[0].subtitle" class="text-xs text-gray-500 text-center mb-3">{{ displayItems[0].subtitle }}</p>
          <div 
            class="rounded-lg px-4 py-2 shadow-lg"
            style="background: linear-gradient(to right, #facc15, #f97316);"
          >
            <span class="text-lg font-bold text-white">{{ formatScore(displayItems[0].score) }}</span>
            <span v-if="scoreUnit" class="text-sm text-yellow-100 ml-1">{{ scoreUnit }}</span>
          </div>
        </div>

        <!-- 第三名 -->
        <div class="flex flex-col items-center pt-8" :style="animationStyle(2)">
          <div class="relative mb-4">
            <div class="w-16 h-16 rounded-2xl overflow-hidden border-4 border-amber-400 shadow-lg">
              <img 
                v-if="displayItems[2].avatar" 
                :src="displayItems[2].avatar" 
                :alt="displayItems[2].name"
                class="w-full h-full object-cover"
                @error="handleImageError"
              />
              <div 
                v-else 
                class="w-full h-full flex items-center justify-center text-white font-bold text-lg"
                style="background: linear-gradient(to bottom right, #fbbf24, #f97316);"
              >
                {{ getInitials(displayItems[2].name) }}
              </div>
            </div>
            <div 
              class="absolute -top-2 -right-2 w-8 h-8 rounded-full flex items-center justify-center shadow-lg"
              style="background: linear-gradient(to bottom right, #fbbf24, #f97316);"
            >
              <span class="text-white font-bold text-sm">3</span>
            </div>
            <div v-if="showOnlineStatus && displayItems[2].online" class="absolute -bottom-1 -right-1 w-4 h-4 bg-green-500 border-2 border-white rounded-full"></div>
          </div>
          <h4 class="font-semibold text-gray-900 text-center mb-1">{{ displayItems[2].name }}</h4>
          <p v-if="displayItems[2].subtitle" class="text-xs text-gray-500 text-center mb-2">{{ displayItems[2].subtitle }}</p>
          <div class="bg-amber-100 rounded-lg px-3 py-1">
            <span class="text-sm font-bold text-amber-700">{{ formatScore(displayItems[2].score) }}</span>
            <span v-if="scoreUnit" class="text-xs text-amber-600 ml-1">{{ scoreUnit }}</span>
          </div>
        </div>
      </div>
    </div>

    <!-- 其他排名列表 -->
    <div class="space-y-2">
      <div 
        v-for="(item, index) in displayItems.slice(3)" 
        :key="item.id || index"
        :class="itemClass(index + 3)"
        :style="animationStyle(index + 3)"
      >
        <!-- 排名 -->
        <div class="flex items-center justify-center w-10 h-10 bg-gray-100 rounded-xl mr-4 flex-shrink-0">
          <span class="text-sm font-bold text-gray-600">{{ index + 4 }}</span>
        </div>

        <!-- 用户头像 -->
        <div class="relative mr-4 flex-shrink-0">
          <div class="w-12 h-12 rounded-xl overflow-hidden border-2 border-gray-200">
            <img 
              v-if="item.avatar" 
              :src="item.avatar" 
              :alt="item.name"
              class="w-full h-full object-cover"
              @error="handleImageError"
            />
            <div 
              v-else 
              class="w-full h-full flex items-center justify-center text-white font-semibold"
              style="background: linear-gradient(to bottom right, #9ca3af, #6b7280);"
            >
              {{ getInitials(item.name) }}
            </div>
          </div>
          <!-- 在线状态指示器 -->
          <div v-if="showOnlineStatus && item.online" class="absolute -bottom-0.5 -right-0.5 w-3 h-3 bg-green-500 border-2 border-white rounded-full"></div>
        </div>

        <!-- 用户信息 -->
        <div class="flex-1 min-w-0">
          <div class="flex items-center justify-between">
            <div class="min-w-0 flex-1">
              <h4 class="font-semibold text-gray-900 truncate">{{ item.name }}</h4>
              <p v-if="item.subtitle" class="text-sm text-gray-500 truncate">{{ item.subtitle }}</p>
            </div>
            <div class="text-right ml-4 flex items-center space-x-3">
              <!-- 变化指示器 -->
              <div v-if="item.change" :class="changeClass(item.change)">
                <svg v-if="item.change > 0" class="w-3 h-3" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M5.293 7.707a1 1 0 010-1.414l4-4a1 1 0 011.414 0l4 4a1 1 0 01-1.414 1.414L11 5.414V17a1 1 0 11-2 0V5.414L6.707 7.707a1 1 0 01-1.414 0z" clip-rule="evenodd"></path>
                </svg>
                <svg v-else class="w-3 h-3" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M14.707 12.293a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 111.414-1.414L9 14.586V3a1 1 0 112 0v11.586l2.293-2.293a1 1 0 011.414 0z" clip-rule="evenodd"></path>
                </svg>
                <span class="text-xs font-medium">{{ Math.abs(item.change) }}</span>
              </div>
              
              <!-- 分数 -->
              <div class="text-right">
                <div class="font-bold text-gray-900">
                  {{ formatScore(item.score) }}
                  <span v-if="scoreUnit" class="text-sm text-gray-500 font-normal ml-1">{{ scoreUnit }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- 操作按钮 -->
        <div v-if="showActions" class="ml-4 flex space-x-2">
          <button 
            @click="handleViewProfile(item)"
            class="w-9 h-9 bg-gray-50 hover:bg-gray-100 border border-gray-200 rounded-lg flex items-center justify-center transition-all duration-200 hover:shadow-md group"
            title="查看资料"
          >
            <svg class="w-4 h-4 text-gray-500 group-hover:text-gray-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- 加载更多 -->
    <div v-if="showLoadMore && hasMore" class="mt-8 text-center">
      <button 
        @click="handleLoadMore"
        :disabled="loading"
        class="px-6 py-3 bg-white border border-gray-200 text-gray-700 hover:text-gray-900 hover:bg-gray-50 hover:border-gray-300 rounded-xl transition-all duration-200 disabled:opacity-50 font-medium"
      >
        {{ loading ? '加载中...' : '查看更多' }}
      </button>
    </div>

    <!-- 空状态 -->
    <div v-if="!loading && displayItems.length === 0" class="text-center py-16">
      <div class="w-16 h-16 bg-gray-100 rounded-2xl mx-auto mb-4 flex items-center justify-center">
        <svg class="w-8 h-8 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path>
        </svg>
      </div>
      <h3 class="text-lg font-semibold text-gray-900 mb-2">暂无排行数据</h3>
      <p class="text-gray-500">等待用户数据更新</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const props = defineProps({
  // 数据
  items: { type: Array, default: () => [] },
  title: { type: String, default: '' },
  scoreUnit: { type: String, default: '' },
  
  // 样式
  variant: { type: String, default: 'default' }, // default, compact, card
  size: { type: String, default: 'md' }, // sm, md, lg
  
  // 功能
  showOnlineStatus: { type: Boolean, default: false },
  showActions: { type: Boolean, default: false },
  showRefresh: { type: Boolean, default: false },
  showLoadMore: { type: Boolean, default: false },
  animated: { type: Boolean, default: true },
  
  // 分页
  pageSize: { type: Number, default: 10 },
  hasMore: { type: Boolean, default: false },
  loading: { type: Boolean, default: false },
});

const emit = defineEmits(['refresh', 'loadMore', 'viewProfile']);

// 显示的项目（考虑分页）
const displayItems = computed(() => {
  return props.items.slice(0, props.pageSize);
});

// 排行榜容器样式
const leaderboardClass = computed(() => {
  const baseClasses = ['leaderboard'];
  
  if (props.variant === 'card') {
    baseClasses.push('bg-white rounded-2xl p-8 shadow-lg border border-gray-100');
  } else if (props.variant === 'compact') {
    baseClasses.push('bg-gray-50 rounded-2xl p-6');
  } else {
    baseClasses.push('bg-white rounded-2xl p-8 shadow-sm border border-gray-100');
  }
  
  return baseClasses;
});

// 排行项样式
const itemClass = (index) => {
  const baseClasses = [
    'flex items-center p-4 rounded-2xl transition-all duration-300',
    'hover:bg-gray-50 hover:shadow-md hover:scale-102',
    'border border-gray-100 bg-white'
  ];
  
  if (props.variant === 'compact') {
    baseClasses.push('p-3');
  }
  
  return baseClasses;
};

// 变化指示器样式
const changeClass = (change) => {
  const baseClasses = ['flex items-center space-x-1 px-2 py-1 rounded-lg text-xs font-medium'];
  
  if (change > 0) {
    baseClasses.push('bg-green-100 text-green-700');
  } else {
    baseClasses.push('bg-red-100 text-red-700');
  }
  
  return baseClasses;
};

// 动画样式
const animationStyle = (index) => {
  if (!props.animated) return {};
  
  return {
    animationDelay: `${index * 100}ms`,
    animationFillMode: 'both',
    animationName: 'slideInUp',
    animationDuration: '0.6s',
    animationTimingFunction: 'cubic-bezier(0.4, 0, 0.2, 1)'
  };
};

// 工具函数
const formatScore = (score) => {
  if (score >= 1000000) {
    return (score / 1000000).toFixed(1) + 'M';
  } else if (score >= 1000) {
    return (score / 1000).toFixed(1) + 'K';
  }
  return score.toString();
};

const getInitials = (name) => {
  return name.split(' ').map(n => n[0]).join('').toUpperCase().slice(0, 2);
};

const handleImageError = (event) => {
  event.target.style.display = 'none';
};

// 事件处理
const handleRefresh = () => {
  emit('refresh');
};

const handleLoadMore = () => {
  emit('loadMore');
};

const handleViewProfile = (item) => {
  emit('viewProfile', item);
};
</script>

<style scoped>
.leaderboard {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
}

.hover\:scale-102:hover {
  transform: scale(1.02);
}

/* 入场动画 */
@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 头像悬停效果 */
.leaderboard img:hover {
  transform: scale(1.05);
  transition: transform 0.2s ease-in-out;
}

/* 自定义阴影 */
.leaderboard .shadow-lg {
  box-shadow: 
    0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.leaderboard .shadow-xl {
  box-shadow: 
    0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

/* 渐变动画 */
@keyframes shimmer {
  0% {
    background-position: -200px 0;
  }
  100% {
    background-position: calc(200px + 100%) 0;
  }
}

.leaderboard .bg-gradient-to-r {
  background-size: 200px 100%;
  background-image: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.2),
    transparent
  );
  animation: shimmer 2s infinite;
}
</style> 