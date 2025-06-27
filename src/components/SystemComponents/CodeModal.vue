<template>
  <transition
    name="modal-fade"
    enter-active-class="transition-all duration-300 ease-out"
    leave-active-class="transition-all duration-200 ease-in"
    enter-from-class="opacity-0 scale-95"
    leave-to-class="opacity-0 scale-95"
  >
    <div
      v-if="visible"
      class="fixed inset-0 bg-white/20 backdrop-blur-md flex items-center justify-center z-50 p-4"
      @click.self="close"
    >
      <div
        class="bg-white rounded-2xl shadow-2xl w-full max-w-4xl flex flex-col border border-slate-200 overflow-hidden transform transition-all duration-300"
      >
        <!-- Header -->
        <div class="flex justify-between items-center px-6 py-5 border-b border-slate-100 bg-slate-50/50">
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-slate-900 rounded-lg flex items-center justify-center">
              <Copy :size="16" class="text-white" />
            </div>
            <h3 class="text-xl font-semibold text-slate-900 m-0">{{ title }}</h3>
          </div>
          <button
            class="w-8 h-8 bg-slate-100 hover:bg-slate-200 rounded-lg flex items-center justify-center cursor-pointer transition-colors duration-200 border-none"
            @click="close"
          >
            <X :size="16" class="text-slate-600" />
          </button>
        </div>

        <!-- Tabs -->
        <div v-if="codeTabs.length > 1" class="flex border-b border-slate-100 bg-white px-6">
          <button
            v-for="(tab, index) in codeTabs"
            :key="index"
            class="px-4 py-3 cursor-pointer bg-transparent border-none text-slate-600 text-sm font-medium relative transition-all duration-200 ease hover:text-slate-900"
            :class="{ 
              'text-slate-900 bg-slate-50/50': activeTabIndex === index
            }"
            @click="switchTab(index)"
          >
            {{ tab.title }}
            <!-- Tab indicator dot -->
            <div 
              class="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-1.5 h-1.5 rounded-full transition-all duration-300 ease-in-out"
              :class="{ 
                'bg-slate-900 scale-125': activeTabIndex === index,
                'bg-transparent': activeTabIndex !== index 
              }"
            ></div>
          </button>
        </div>

        <!-- Code Content -->
        <div class="overflow-hidden bg-slate-900">
          <div class="overflow-y-auto max-h-[60vh] relative">
            <!-- Language indicator -->
            <div class="absolute top-4 right-4 z-10">
              <span class="px-3 py-1 bg-slate-800 text-slate-300 text-xs font-mono rounded-md border border-slate-700">
                {{ activeLanguage }}
              </span>
            </div>
            
            <pre class="bg-slate-900 text-slate-100 p-6 m-0 whitespace-pre-wrap break-words">
              <code ref="codeBlock" :class="`language-${activeLanguage} font-mono text-sm leading-relaxed`">{{ activeCode }}</code>
            </pre>
          </div>
        </div>

        <!-- Footer -->
        <div class="px-6 py-4 bg-slate-50/50 border-t border-slate-100 flex justify-between items-center">
          <div class="text-xs text-slate-500 font-mono">
            {{ activeCode.split('\n').length }} 行 · {{ activeCode.length }} 字符
          </div>
          
          <div class="flex items-center space-x-3">
            <button
              class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 border-none rounded-lg cursor-pointer text-sm font-medium transition-colors duration-200 flex items-center space-x-2"
              @click="close"
            >
              <span>关闭</span>
            </button>
            
            <button
              class="px-4 py-2 bg-slate-900 hover:bg-slate-800 text-white border-none rounded-lg cursor-pointer text-sm font-medium transition-all duration-200 flex items-center space-x-2 shadow-lg"
              :class="{ 
                'bg-green-600 hover:bg-green-700': copied,
                'scale-95': copied 
              }"
              @click="copyCode"
            >
              <Copy :size="14" v-if="!copied" />
              <Check :size="14" v-else class="text-green-100" />
              <span>{{ copied ? '已复制!' : '复制代码' }}</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { ref, watch, computed, nextTick } from 'vue';
import { Copy, Check, X } from 'lucide-vue-next';
import hljs from 'highlight.js/lib/core';
import javascript from 'highlight.js/lib/languages/javascript';
import xml from 'highlight.js/lib/languages/xml'; // For Vue templates
import css from 'highlight.js/lib/languages/css';

// Re-adding the style import here for better encapsulation
import 'highlight.js/styles/atom-one-dark.css';

hljs.registerLanguage('javascript', javascript);
hljs.registerLanguage('xml', xml);
hljs.registerLanguage('css', css);

const props = defineProps({
  visible: { type: Boolean, required: true },
  title: { type: String, default: 'Code' },
  codeTabs: { type: Array, required: true, default: () => [] },
});

const emit = defineEmits(['close']);

const activeTabIndex = ref(0);
const codeBlock = ref(null);
const copied = ref(false);

const activeTab = computed(() => props.codeTabs[activeTabIndex.value] || { code: '', language: 'plaintext' });
const activeCode = computed(() => activeTab.value.code);
const activeLanguage = computed(() => activeTab.value.language);

const switchTab = (index) => {
  if (activeTabIndex.value === index) return;
  activeTabIndex.value = index;
};

const highlightCode = async () => {
  await nextTick();
  if (codeBlock.value) {
    delete codeBlock.value.dataset.highlighted;
    hljs.highlightElement(codeBlock.value);
  }
};

watch([() => props.visible, activeTabIndex], ([newVisible]) => {
  if (newVisible) {
    highlightCode();
  }
}, { immediate: true });

watch(() => props.visible, (newVal) => {
  if (newVal) {
    copied.value = false;
    if (props.codeTabs.length > 0) {
      activeTabIndex.value = 0;
    }
  }
});

const close = () => {
  emit('close');
};

const copyCode = async () => {
  if (copied.value) return;
  try {
    await navigator.clipboard.writeText(activeCode.value);
    copied.value = true;
    setTimeout(() => { copied.value = false; }, 2000);
  } catch (err) {
    console.error('Failed to copy: ', err);
  }
};
</script>

<style scoped>
/* 自定义滚动条 */
.overflow-y-auto::-webkit-scrollbar {
  width: 6px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: #374151;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background: #6b7280;
  border-radius: 3px;
}

.overflow-y-auto::-webkit-scrollbar-thumb:hover {
  background: #9ca3af;
}
</style>

