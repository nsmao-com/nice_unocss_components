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
        @click.self="emit('close')"
      >
      <div 
        class="bg-white rounded-2xl shadow-2xl w-full max-w-4xl flex flex-col border border-slate-200 overflow-hidden transform transition-all duration-300"
      >
        <!-- 头部 -->
        <div class="flex justify-between items-center px-6 py-5 border-b border-slate-100 bg-slate-50/50">
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">
              <Info :size="16" class="text-white" />
            </div>
            <div>
              <h3 class="text-xl font-semibold text-slate-900 m-0">{{ title }} 参数说明</h3>
              <p class="text-sm text-slate-600 m-0">查看所有可用的配置参数</p>
            </div>
          </div>
          <button 
            @click="emit('close')"
            class="w-8 h-8 bg-slate-100 hover:bg-slate-200 rounded-lg flex items-center justify-center cursor-pointer transition-colors duration-200 border-none"
          >
            <X :size="16" class="text-slate-600" />
          </button>
        </div>

        <!-- 内容区域 -->
        <div class="p-6 overflow-y-auto max-h-[60vh]">
          <div class="overflow-x-auto">
            <table class="w-full border border-slate-200 rounded-lg overflow-hidden">
              <thead class="bg-slate-50">
                <tr>
                  <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">参数名</th>
                  <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">类型</th>
                  <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">默认值</th>
                  <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">必需</th>
                  <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">说明</th>
                </tr>
              </thead>
              <tbody>
                <tr 
                  v-for="(param, index) in parameters" 
                  :key="index"
                  class="hover:bg-slate-50 transition-colors"
                >
                  <td class="px-4 py-3 text-sm font-mono text-blue-600 border-b border-slate-100">
                    {{ param.name }}
                  </td>
                  <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                    <span class="px-2 py-1 bg-slate-100 text-slate-700 rounded text-xs font-mono">
                      {{ param.type }}
                    </span>
                  </td>
                  <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                    <code v-if="param.default !== undefined" class="px-2 py-1 bg-amber-50 text-amber-700 rounded text-xs">
                      {{ param.default }}
                    </code>
                    <span v-else class="text-slate-400">-</span>
                  </td>
                  <td class="px-4 py-3 text-sm border-b border-slate-100">
                    <span 
                      :class="[
                        'px-2 py-1 rounded-full text-xs font-medium',
                        param.required 
                          ? 'bg-red-100 text-red-700' 
                          : 'bg-green-100 text-green-700'
                      ]"
                    >
                      {{ param.required ? '是' : '否' }}
                    </span>
                  </td>
                  <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                    {{ param.description }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>

          <!-- 事件说明 -->
          <div v-if="events && events.length > 0" class="mt-8">
            <h3 class="text-lg font-semibold text-slate-900 mb-4 flex items-center">
              <Zap :size="18" class="mr-2 text-yellow-600" />
              事件说明
            </h3>
            <div class="overflow-x-auto">
              <table class="w-full border border-slate-200 rounded-lg overflow-hidden">
                <thead class="bg-yellow-50">
                  <tr>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">事件名</th>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">参数</th>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">说明</th>
                  </tr>
                </thead>
                <tbody>
                  <tr 
                    v-for="(event, index) in events" 
                    :key="index"
                    class="hover:bg-yellow-50 transition-colors"
                  >
                    <td class="px-4 py-3 text-sm font-mono text-blue-600 border-b border-slate-100">
                      @{{ event.name }}
                    </td>
                    <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                      <code v-if="event.params" class="px-2 py-1 bg-slate-100 text-slate-700 rounded text-xs">
                        {{ event.params }}
                      </code>
                      <span v-else class="text-slate-400">-</span>
                    </td>
                    <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                      {{ event.description }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>

          <!-- 插槽说明 -->
          <div v-if="slots && slots.length > 0" class="mt-8">
            <h3 class="text-lg font-semibold text-slate-900 mb-4 flex items-center">
              <Layers :size="18" class="mr-2 text-purple-600" />
              插槽说明
            </h3>
            <div class="overflow-x-auto">
              <table class="w-full border border-slate-200 rounded-lg overflow-hidden">
                <thead class="bg-purple-50">
                  <tr>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">插槽名</th>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">作用域</th>
                    <th class="px-4 py-3 text-left text-sm font-medium text-slate-700 border-b border-slate-200">说明</th>
                  </tr>
                </thead>
                <tbody>
                  <tr 
                    v-for="(slot, index) in slots" 
                    :key="index"
                    class="hover:bg-purple-50 transition-colors"
                  >
                    <td class="px-4 py-3 text-sm font-mono text-blue-600 border-b border-slate-100">
                      #{{ slot.name }}
                    </td>
                    <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                      <code v-if="slot.scope" class="px-2 py-1 bg-slate-100 text-slate-700 rounded text-xs">
                        {{ slot.scope }}
                      </code>
                      <span v-else class="text-slate-400">-</span>
                    </td>
                    <td class="px-4 py-3 text-sm text-slate-600 border-b border-slate-100">
                      {{ slot.description }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- 底部 -->
        <div class="px-6 py-4 bg-slate-50/50 border-t border-slate-100 flex justify-between items-center">
          <div class="text-xs text-slate-500 font-mono">
            <span class="inline-flex items-center">
              <FileText :size="14" class="mr-1" />
              共 {{ parameters.length }} 个参数
              <span v-if="events && events.length > 0" class="ml-2">
                · {{ events.length }} 个事件
              </span>
              <span v-if="slots && slots.length > 0" class="ml-2">
                · {{ slots.length }} 个插槽
              </span>
            </span>
          </div>
          <div class="flex items-center space-x-3">
            <button 
              @click="emit('close')"
              class="px-4 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 border-none rounded-lg cursor-pointer text-sm font-medium transition-colors duration-200 flex items-center space-x-2"
            >
              <span>关闭</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { X, Info, Zap, Layers, FileText } from 'lucide-vue-next';

defineProps({
  visible: {
    type: Boolean,
    default: false,
  },
  title: {
    type: String,
    required: true,
  },
  parameters: {
    type: Array,
    required: true,
  },
  events: {
    type: Array,
    default: () => [],
  },
  slots: {
    type: Array,
    default: () => [],
  },
});

const emit = defineEmits(['close']);
</script>

<style scoped>
/* 自定义滚动条 */
.overflow-y-auto::-webkit-scrollbar {
  width: 6px;
}

.overflow-y-auto::-webkit-scrollbar-track {
  background: #f1f5f9;
  border-radius: 3px;
}

.overflow-y-auto::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 3px;
}

.overflow-y-auto::-webkit-scrollbar-thumb:hover {
  background: #94a3b8;
}
</style> 