<template>
  <div class="min-h-screen bg-slate-50">
    <!-- Header -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-16">
          <div class="flex items-center space-x-3">
            <div class="w-8 h-8 bg-slate-900 rounded-lg flex items-center justify-center">
              <Component :size="20" class="text-white" />
            </div>
            <div>
              <h1 class="text-xl font-bold text-slate-900">Nice Components</h1>
              <p class="text-xs text-slate-500">Vue 3 组件库</p>
            </div>
          </div>
          <nav class="hidden md:flex items-center space-x-8">
            <a href="https://www.nsmao.com" target="_blank" class="text-slate-600 hover:text-slate-900 font-medium transition-colors">奈斯猫</a>
            <a href="#components" class="text-slate-600 hover:text-slate-900 font-medium transition-colors">组件</a>
            <a href="https://github.com/nsmao-com/nice_unocss_components" target="_blank" class="text-slate-600 hover:text-slate-900 font-medium transition-colors">GitHub</a>
          </nav>
        </div>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-20">
        <div class="text-center">
          <h1 class="text-4xl md:text-6xl font-bold text-slate-900 mb-6 leading-tight">
            精美简约的
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-slate-900 to-slate-600">Vue 3 组件</span>
          </h1>
          <p class="text-xl text-slate-600 mb-8 max-w-2xl mx-auto leading-relaxed">
            使用 UnoCSS 构建的现代化组件库，专注于简约设计和优秀的用户体验
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <a href="#components" class="px-8 py-3 bg-slate-900 text-white rounded-lg font-medium hover:bg-slate-800 transition-colors shadow-lg">
              开始使用
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="py-20 bg-slate-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-slate-900 mb-4">为什么选择 Nice Components</h2>
          <p class="text-lg text-slate-600 max-w-2xl mx-auto">专为现代 Web 应用设计的组件库</p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                      <div class="bg-white rounded-xl p-8 shadow-sm border border-slate-200 hover:shadow-md transition-shadow">
              <div class="w-12 h-12 bg-slate-100 rounded-lg flex items-center justify-center mb-6">
                <Wrench :size="24" class="text-slate-600" />
              </div>
              <h3 class="text-xl font-semibold text-slate-900 mb-3">现代化设计</h3>
              <p class="text-slate-600 leading-relaxed">简约而不简单，每个组件都经过精心设计，符合现代 UI 设计趋势</p>
            </div>
            
            <div class="bg-white rounded-xl p-8 shadow-sm border border-slate-200 hover:shadow-md transition-shadow">
              <div class="w-12 h-12 bg-slate-100 rounded-lg flex items-center justify-center mb-6">
                <Globe :size="24" class="text-slate-600" />
              </div>
              <h3 class="text-xl font-semibold text-slate-900 mb-3">开箱即用</h3>
              <p class="text-slate-600 leading-relaxed">使用 UnoCSS 构建，无需额外样式配置，复制代码即可使用</p>
            </div>
            
            <div class="bg-white rounded-xl p-8 shadow-sm border border-slate-200 hover:shadow-md transition-shadow">
              <div class="w-12 h-12 bg-slate-100 rounded-lg flex items-center justify-center mb-6">
                <HeartHandshake :size="24" class="text-slate-600" />
              </div>
              <h3 class="text-xl font-semibold text-slate-900 mb-3">高质量代码</h3>
              <p class="text-slate-600 leading-relaxed">基于 Vue 3 Composition API，代码清晰易懂，便于定制和扩展</p>
            </div>
        </div>
      </div>
    </section>

    <!-- Components Section -->
    <section id="components" class="py-20 bg-white">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-slate-900 mb-4">组件展示</h2>
          <p class="text-lg text-slate-600">精心设计的 Vue 3 组件集合</p>
        </div>

        <div class="masonry-container">
          <!-- Pagination Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <ChevronRight :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Pagination</h3>
                    <p class="text-sm text-slate-500">滑块式分页组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Pagination')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openPaginationModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6 space-y-8">
              <!-- 基础分页 -->
              <div>
                <h4 class="text-sm font-medium text-slate-700 mb-3">基础分页</h4>
                <pagination 
                  v-model:currentPage="paginationCurrentPage"
                  :totalPages="20"
                />
                <div class="text-xs text-slate-500 mt-2">当前页: {{ paginationCurrentPage }}/20</div>
              </div>
              
              <!-- 不同尺寸 -->
              <div>
                <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
                <div class="space-y-3">
                  <div>
                    <span class="text-xs text-slate-500 mr-2">小尺寸:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="10"
                      size="sm"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">大尺寸:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="10"
                      size="lg"
                    />
                  </div>
                </div>
              </div>
              
              <!-- 不同变体 -->
              <div>
                <h4 class="text-sm font-medium text-slate-700 mb-3">不同变体</h4>
                <div class="space-y-3">
                  <div>
                    <span class="text-xs text-slate-500 mr-2">主要样式:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      variant="primary"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">极简样式:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      variant="minimal"
                    />
                  </div>
                </div>
              </div>
              
              <!-- 功能选项 -->
              <div>
                <h4 class="text-sm font-medium text-slate-700 mb-3">功能选项</h4>
                <div class="space-y-3">
                  <div>
                    <span class="text-xs text-slate-500 mr-2">紧凑模式:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="10"
                      :compact="true"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">紧凑+圆角:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="10"
                      :compact="true"
                      :rounded="true"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">无箭头:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      :showArrows="false"
                    />
                  </div>

                  <div>
                    <span class="text-xs text-slate-500 mr-2">紧凑模式:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      :compact="true"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">圆形样式:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      :rounded="true"
                    />
                  </div>
                  <div>
                    <span class="text-xs text-slate-500 mr-2">紧凑+圆形:</span>
                    <pagination 
                      v-model:currentPage="paginationCurrentPage"
                      :totalPages="8"
                      :compact="true"
                      :rounded="true"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Slider Tab Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Component :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Slider Tab</h3>
                    <p class="text-sm text-slate-500">平滑动画的选项卡组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('SliderTab')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openSliderTabModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <!-- Horizontal Tabs -->
              <div class="mb-6">
                <h4 class="text-sm font-medium text-slate-700 mb-3">水平模式</h4>
                <slider-tab :tabs="tabs" v-model="activeTab" :vertical="false" />
                <div class="bg-slate-50 rounded-lg p-4 mt-3 min-h-16 flex items-center justify-center">
                  <div class="text-center text-slate-600 text-sm">
                    当前选中: {{ tabs[activeTab]?.title }}
                  </div>
                </div>
              </div>
              
              <!-- Vertical Tabs -->
              <div class="mb-4">
                <h4 class="text-sm font-medium text-slate-700 mb-3">垂直模式</h4>
                <div class="flex gap-4">
                  <slider-tab :tabs="tabs" v-model="activeTab" :vertical="true" />
                  <div class="flex-1 bg-slate-50 rounded-lg p-4 min-h-24 flex items-center justify-center">
                    <div class="text-center text-slate-600 text-sm">
                      当前选中: {{ tabs[activeTab]?.title }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Carousel Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Image :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Carousel</h3>
                    <p class="text-sm text-slate-500">自动播放的轮播图组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Carousel')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openCarouselModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <carousel 
                :items="carouselItems" 
                :interval="carouselInterval" 
                :autoplay="carouselAutoplay"
                :autoplay-start="carouselAutoplayStart"
                :pause-on-hover="carouselPauseOnHover"
                :show-arrows="true"
                :show-indicators="true"
                :show-play-pause="true"
              />
              
              <!-- 控制按钮区域 -->
              <div class="mt-4 space-y-3">
                <div class="flex flex-wrap gap-2 text-sm">
                  <button 
                    @click="carouselAutoplay = !carouselAutoplay"
                    :class="[
                      'px-3 py-1.5 rounded-md transition-colors duration-200 font-medium',
                      carouselAutoplay 
                        ? 'bg-blue-100 text-blue-700' 
                        : 'bg-slate-200 text-slate-600'
                    ]"
                  >
                    自动播放: {{ carouselAutoplay ? '开' : '关' }}
                  </button>
                  
                  <button 
                    @click="carouselAutoplayStart = !carouselAutoplayStart"
                    :class="[
                      'px-3 py-1.5 rounded-md transition-colors duration-200 font-medium',
                      carouselAutoplayStart 
                        ? 'bg-green-100 text-green-700' 
                        : 'bg-slate-200 text-slate-600'
                    ]"
                  >
                    自动开始: {{ carouselAutoplayStart ? '是' : '否' }}
                  </button>
                  
                  <button 
                    @click="carouselPauseOnHover = !carouselPauseOnHover"
                    :class="[
                      'px-3 py-1.5 rounded-md transition-colors duration-200 font-medium',
                      carouselPauseOnHover 
                        ? 'bg-purple-100 text-purple-700' 
                        : 'bg-slate-200 text-slate-600'
                    ]"
                  >
                    悬停暂停: {{ carouselPauseOnHover ? '是' : '否' }}
                  </button>
                  
                  <select 
                    v-model.number="carouselInterval"
                    class="px-3 py-1.5 rounded-md bg-orange-100 text-orange-700 font-medium outline-none border-none"
                  >
                    <option :value="2000">间隔: 2秒</option>
                    <option :value="3000">间隔: 3秒</option>
                    <option :value="4000">间隔: 4秒</option>
                    <option :value="5000">间隔: 5秒</option>
                    <option :value="6000">间隔: 6秒</option>
                  </select>
                </div>
                
                <div class="text-xs text-slate-500 text-center">
                  当前设置: {{ carouselAutoplay ? '自动播放' : '手动模式' }} · 
                  {{ carouselPauseOnHover ? '悬停暂停' : '不暂停' }} · 
                  {{ carouselInterval / 1000 }}秒间隔
                </div>
              </div>
            </div>
          </div>

          <!-- RippleButton Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <MousePointer :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">RippleButton</h3>
                    <p class="text-sm text-slate-500">带涟漪动画效果的按钮组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('RippleButton')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openRippleButtonModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-4">
                <!-- 不同变体的按钮 -->
                <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
                  <ripple-button text="Primary" variant="primary" />
                  <ripple-button text="Secondary" variant="secondary" />
                  <ripple-button text="Outline" variant="outline" />
                  <ripple-button text="Ghost" variant="ghost" />
                  <ripple-button text="Danger" variant="danger" />
                  <ripple-button text="Success" variant="success" />
                </div>
                
                <!-- 不同尺寸的按钮 -->
                <div class="flex flex-wrap items-center gap-3">
                  <ripple-button text="Small" size="sm" />
                  <ripple-button text="Medium" size="md" />
                  <ripple-button text="Large" size="lg" />
                  <ripple-button text="Extra Large" size="xl" />
                </div>
                
                <!-- 特殊形状的按钮 -->
                <div class="flex flex-wrap items-center gap-3">
                  <ripple-button text="圆形按钮" :rounded="true" />
                  <ripple-button text="全宽按钮" :full-width="true" />
                </div>
                
                <!-- 带图标的按钮 -->
                <div class="flex flex-wrap items-center gap-3">
                  <ripple-button text="下载" :icon="Download" variant="outline" />
                  <ripple-button text="保存" :icon="Save" variant="success" />
                  <ripple-button text="删除" :icon="Trash2" variant="danger" />
                  
                  <!-- 使用图标插槽 -->
                  <ripple-button text="设置" variant="secondary">
                    <template #icon>
                      <Settings :size="16" />
                    </template>
                  </ripple-button>
                  
                  <!-- 只有图标的按钮（自动圆形） -->
                  <ripple-button variant="ghost" size="sm">
                    <template #icon>
                      <Heart :size="14" />
                    </template>
                  </ripple-button>
                  
                  <ripple-button variant="primary">
                    <template #icon>
                      <Share2 :size="16" />
                    </template>
                  </ripple-button>
                  
                  <ripple-button variant="success" size="lg">
                    <template #icon>
                      <Plus :size="20" />
                    </template>
                  </ripple-button>
                </div>
              </div>
              
              <div class="mt-4 text-xs text-slate-500 text-center">
                点击任意按钮查看涟漪动画效果
              </div>
            </div>
          </div>

          <!-- Badge Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Component :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Badge</h3>
                    <p class="text-sm text-slate-500">多样式的徽章组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Badge')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openBadgeModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 数字徽章 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">数字徽章</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=40&h=40&fit=crop&crop=face&auto=format" alt="用户头像" class="w-10 h-10 rounded-full object-cover" />
                      <badge :content="5" variant="danger" class="absolute -top-1 -right-1" />
                    </div>
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=40&h=40&fit=crop&crop=face&auto=format" alt="用户头像" class="w-10 h-10 rounded-full object-cover" />
                      <badge :content="99" variant="danger" class="absolute -top-0.5 -right-0.5" />
                    </div>
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=40&h=40&fit=crop&crop=face&auto=format" alt="用户头像" class="w-10 h-10 rounded-full object-cover" />
                      <badge :content="999" :max="99" variant="danger" class="absolute -top-0.5 -right-0.5" />
                    </div>
                  </div>
                </div>

                <!-- 状态点 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">在线状态</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=40&h=40&fit=crop&crop=face&auto=format" alt="用户头像" class="w-10 h-10 rounded-full object-cover" />
                      <badge dot variant="success" class="absolute bottom-0.5 right-0.5" />
                    </div>
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1500648767791-00dcc994a43e?w=40&h=40&fit=crop&crop=face&auto=format" alt="用户头像" class="w-10 h-10 rounded-full object-cover" />
                      <badge dot variant="warning" class="absolute bottom-0.5 right-0.5" />
                    </div>
                  </div>
                </div>

                <!-- 文字徽章 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">标签徽章</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1517336714731-489689fd1ca8?w=50&h=50&fit=crop&auto=format" alt="产品图片" class="w-12 h-12 rounded-lg object-cover border-2 border-slate-200" />
                      <badge content="NEW" variant="danger" size="sm" square class="absolute -top-1 -right-1" />
                    </div>
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?w=50&h=50&fit=crop&auto=format" alt="产品图片" class="w-12 h-12 rounded-lg object-cover border-2 border-slate-200" />
                      <badge content="HOT" variant="warning" size="sm" square class="absolute -top-1 -right-1" />
                    </div>
                    <div class="relative">
                      <img src="https://images.unsplash.com/photo-1503602642458-232111445657?w=50&h=50&fit=crop&auto=format" alt="产品图片" class="w-12 h-12 rounded-lg object-cover border-2 border-slate-200" />
                      <badge content="99+" variant="danger" size="sm" class="absolute -top-1 -right-1" />
                    </div>
                  </div>
                </div>

                <!-- 样式变体 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">样式变体</h4>
                  <div class="flex items-center gap-3 flex-wrap">
                    <badge content="5" variant="danger" />
                    <badge content="NEW" variant="danger" square />
                    <badge dot variant="success" />
                    <badge content="HOT" variant="warning" square />
                    <badge content="99+" variant="danger" />
                    <badge content="VIP" variant="primary" square />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                现代化设计的徽章组件，完美适用于头像、产品等场景
              </div>
            </div>
          </div>

          <!-- Checkbox Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Component :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Checkbox</h3>
                    <p class="text-sm text-slate-500">带动画效果的复选框组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Checkbox')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openCheckboxModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 不同变体 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">不同变体</h4>
                  <div class="grid grid-cols-2 gap-4">
                    <checkbox v-model="checkboxStates.default" variant="default" label="Default" />
                    <checkbox v-model="checkboxStates.primary" variant="primary" label="Primary" />
                    <checkbox v-model="checkboxStates.secondary" variant="secondary" label="Secondary" />
                    <checkbox v-model="checkboxStates.success" variant="success" label="Success" />
                    <checkbox v-model="checkboxStates.warning" variant="warning" label="Warning" />
                    <checkbox v-model="checkboxStates.danger" variant="danger" label="Danger" />
                  </div>
                </div>

                <!-- 不同大小 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">不同大小</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <checkbox v-model="checkboxStates.small" size="sm" label="Small" />
                    <checkbox v-model="checkboxStates.medium" size="md" label="Medium" />
                    <checkbox v-model="checkboxStates.large" size="lg" label="Large" />
                  </div>
                </div>

                <!-- 圆形复选框 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">圆形样式</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <checkbox v-model="checkboxStates.roundedPrimary" variant="primary" rounded label="圆形 Primary" />
                    <checkbox v-model="checkboxStates.roundedSuccess" variant="success" rounded label="圆形 Success" />
                    <checkbox v-model="checkboxStates.roundedDanger" variant="danger" rounded label="圆形 Danger" />
                  </div>
                </div>

                <!-- 禁用状态 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">禁用状态</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <checkbox v-model="checkboxStates.disabledUnchecked" disabled label="禁用未选中" />
                    <checkbox v-model="checkboxStates.disabledChecked" disabled label="禁用已选中" />
                  </div>
                </div>

                <!-- 无标签 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">无标签模式</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <checkbox v-model="checkboxStates.noLabel1" variant="primary" />
                    <checkbox v-model="checkboxStates.noLabel2" variant="success" />
                    <checkbox v-model="checkboxStates.noLabel3" variant="danger" />
                    <checkbox v-model="checkboxStates.noLabel4" variant="primary" rounded />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                点击复选框查看平滑的勾选动画效果
              </div>
            </div>
          </div>

          <!-- Radio Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Component :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Radio</h3>
                    <p class="text-sm text-slate-500">带动画效果的单选框组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Radio')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openRadioModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 基础单选组 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">基础选项</h4>
                  <div class="space-x-2">
                    <radio v-model="radioStates.basic" name="basic" value="option1" label="选项 1" />
                    <radio v-model="radioStates.basic" name="basic" value="option2" label="选项 2" />
                    <radio v-model="radioStates.basic" name="basic" value="option3" label="选项 3" />
                  </div>
                  <div class="text-xs text-slate-500">当前选择: {{ radioStates.basic || '无' }}</div>
                </div>

                <!-- 不同变体 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">不同变体</h4>
                  <div class="grid grid-cols-2 gap-4">
                    <radio v-model="radioStates.variants" name="variants" value="default" variant="default" label="Default" />
                    <radio v-model="radioStates.variants" name="variants" value="primary" variant="primary" label="Primary" />
                    <radio v-model="radioStates.variants" name="variants" value="secondary" variant="secondary" label="Secondary" />
                    <radio v-model="radioStates.variants" name="variants" value="success" variant="success" label="Success" />
                    <radio v-model="radioStates.variants" name="variants" value="warning" variant="warning" label="Warning" />
                    <radio v-model="radioStates.variants" name="variants" value="danger" variant="danger" label="Danger" />
                  </div>
                  <div class="text-xs text-slate-500">当前选择: {{ radioStates.variants || '无' }}</div>
                </div>

                <!-- 不同大小 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">不同大小</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <radio v-model="radioStates.sizes" name="sizes" value="sm" size="sm" label="Small" />
                    <radio v-model="radioStates.sizes" name="sizes" value="md" size="md" label="Medium" />
                    <radio v-model="radioStates.sizes" name="sizes" value="lg" size="lg" label="Large" />
                  </div>
                  <div class="text-xs text-slate-500">当前选择: {{ radioStates.sizes || '无' }}</div>
                </div>

                <!-- 禁用状态 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">禁用状态</h4>
                  <div class="space-x-2">
                    <radio v-model="radioStates.disabled" name="disabled" value="option1" disabled label="禁用未选中" />
                    <radio v-model="radioStates.disabled" name="disabled" value="option2" disabled label="禁用已选中" />
                    <radio v-model="radioStates.disabled" name="disabled" value="option3" label="正常选项" />
                  </div>
                </div>

                <!-- 无标签模式 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">无标签模式</h4>
                  <div class="flex items-center gap-6 flex-wrap">
                    <radio v-model="radioStates.noLabel" name="noLabel" value="option1" variant="primary" />
                    <radio v-model="radioStates.noLabel" name="noLabel" value="option2" variant="success" />
                    <radio v-model="radioStates.noLabel" name="noLabel" value="option3" variant="danger" />
                  </div>
                  <div class="text-xs text-slate-500">当前选择: {{ radioStates.noLabel || '无' }}</div>
                </div>

                <!-- 实际应用示例 -->
                <div class="space-y-3">
                  <h4 class="text-sm font-medium text-slate-700">付款方式选择</h4>
                  <div class="space-x-2">
                    <radio v-model="radioStates.payment" name="payment" value="alipay" variant="primary" label="支付宝" />
                    <radio v-model="radioStates.payment" name="payment" value="wechat" variant="success" label="微信支付" />
                    <radio v-model="radioStates.payment" name="payment" value="unionpay" variant="warning" label="银联支付" />
                    <radio v-model="radioStates.payment" name="payment" value="card" variant="secondary" label="银行卡" />
                  </div>
                  <div class="text-xs text-slate-500">选择的付款方式: {{ radioStates.payment || '请选择' }}</div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                点击单选框查看背景填充和圆点出现的动画效果
              </div>
            </div>
          </div>

          <!-- Input Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Type :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Input</h3>
                    <p class="text-sm text-slate-500">现代化输入框组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Input')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openInputModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 固定标签模式 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">固定标签模式</h4>
                  <div class="space-y-4">
                    <Input 
                      v-model="inputValues.email1" 
                      label="Email" 
                      description="请输入您的邮箱地址"
                    />
                    <Input 
                      v-model="inputValues.name" 
                      label="用户名" 
                      description="请输入6-20位字符的用户名"
                      variant="primary"
                    />
                  </div>
                </div>
                
                <!-- 浮动标签模式 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">浮动标签模式</h4>
                  <div class="space-y-4">
                    <Input 
                      v-model="inputValues.email2" 
                      label="Email" 
                      placeholder="请输入邮箱地址"
                    />
                    <Input 
                      v-model="inputValues.website" 
                      label="网站地址" 
                      placeholder="请输入网站URL"
                      variant="success"
                    />
                  </div>
                </div>

                <!-- 验证功能 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">验证功能</h4>
                  <div class="space-y-4">
                    <Input 
                      v-model="inputValues.success" 
                      label="Email验证" 
                      :validationType="'email'"
                      :showValidationIcon="true"
                      placeholder="输入邮箱地址"
                      variant="success"
                    />
                    <Input 
                      v-model="inputValues.phone" 
                      label="电话验证" 
                      :validationType="'phone'"
                      :showValidationIcon="true"
                      placeholder="输入电话号码"
                      variant="warning"
                    />
                  </div>
                </div>

                <!-- 状态示例 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">状态示例</h4>
                  <div class="space-y-4">
                    <Input 
                      v-model="inputValues.errorExample" 
                      label="错误状态" 
                      errorMessage="邮箱格式不正确，请重新输入"
                      placeholder="invalid-email"
                    />
                    <Input 
                      v-model="inputValues.disabled" 
                      label="禁用状态" 
                      :disabled="true"
                      placeholder="Disabled input"
                    />
                  </div>
                </div>

                <!-- 功能增强 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">功能增强</h4>
                  <div class="space-y-4">
                    <Input 
                      v-model="inputValues.search" 
                      label="搜索" 
                      :prefixIcon="Search"
                      :clearable="true"
                      placeholder="搜索内容..."
                    />
                    <Input 
                      v-model="inputValues.password" 
                      label="密码验证" 
                      type="password"
                      :suffixIcon="Lock"
                      :validationType="'password'"
                      :showValidationIcon="true"
                      placeholder="请输入密码"
                    />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                体验浮动标签动画和现代化的输入框设计
              </div>
            </div>
          </div>

          <!-- Input OTP Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Lock :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Input OTP</h3>
                    <p class="text-sm text-slate-500">验证码输入组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('InputOTP')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openInputOTPModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 基础使用 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">基础使用</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.basic" 
                        label="请输入验证码"
                        helpText="6位数字验证码"
                        @complete="handleOTPComplete('basic', $event)"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        当前值: {{ otpValues.basic || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 不同长度 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同长度</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.short" 
                        label="4位验证码"
                        :length="4"
                        variant="primary"
                        @complete="handleOTPComplete('short', $event)"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        当前值: {{ otpValues.short || '无' }}
                      </div>
                    </div>
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.long" 
                        label="8位验证码"
                        :length="8"
                        variant="success"
                        @complete="handleOTPComplete('long', $event)"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        当前值: {{ otpValues.long || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 不同尺寸 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.small" 
                        label="小尺寸"
                        size="sm"
                        :length="4"
                        variant="warning"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.small || '无' }}
                      </div>
                    </div>
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.large" 
                        label="大尺寸"
                        size="lg"
                        :length="5"
                        variant="danger"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.large || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 不同输入类型 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同输入类型</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.numeric" 
                        label="仅数字"
                        type="numeric"
                        :length="6"
                        helpText="只能输入数字0-9"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.numeric || '无' }}
                      </div>
                    </div>
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.alphanumeric" 
                        label="字母数字"
                        type="alphanumeric"
                        :length="6"
                        variant="primary"
                        helpText="可输入字母和数字"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.alphanumeric || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 错误状态 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">自动错误检测</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.error" 
                        label="自动错误检测"
                        helpText="输入部分内容后失焦，会自动显示错误提示"
                        @complete="handleOTPComplete('error', $event)"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.error || '无' }}
                      </div>
                    </div>
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.manualError" 
                        label="手动错误状态"
                        :error="true"
                        errorMessage="验证码错误，请重新输入"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.manualError || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 禁用状态 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">禁用状态</h4>
                  <div class="text-center">
                    <InputOTP 
                      v-model="otpValues.disabled" 
                      label="禁用状态"
                      :disabled="true"
                      helpText="此输入框已禁用"
                    />
                    <div class="mt-2 text-sm text-slate-600">
                      值: {{ otpValues.disabled || '无' }}
                    </div>
                  </div>
                </div>

                <!-- 圆角样式 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">圆角样式</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.rounded" 
                        label="圆形输入框"
                        :rounded="true"
                        variant="primary"
                        helpText="使用rounded参数设置为圆形"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.rounded || '无' }}
                      </div>
                    </div>
                  </div>
                </div>

                <!-- 密码隐藏 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">密码隐藏</h4>
                  <div class="space-y-4">
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.password" 
                        label="密码模式"
                        :password="true"
                        variant="success"
                        helpText="输入内容会显示为圆点"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.password || '无' }}
                      </div>
                    </div>
                    <div class="text-center">
                      <InputOTP 
                        v-model="otpValues.roundedPassword" 
                        label="圆形密码模式"
                        :rounded="true"
                        :password="true"
                        variant="warning"
                        helpText="圆形输入框 + 密码隐藏"
                      />
                      <div class="mt-2 text-sm text-slate-600">
                        值: {{ otpValues.roundedPassword || '无' }}
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                支持自动聚焦、粘贴输入、键盘导航和完成回调的验证码输入组件
              </div>
            </div>
          </div>

          <!-- Alert Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <AlertTriangle :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Alert</h3>
                    <p class="text-sm text-slate-500">多样式的警告提示组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Alert')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openAlertModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-4">
                <!-- 不同变体的Alert -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同类型</h4>
                  <div class="space-y-3">
                    <Alert variant="default" message="This is a default alert" />
                    <Alert variant="primary" message="This is a primary alert" />
                    <Alert variant="secondary" message="This is a secondary alert" />
                    <Alert variant="success" message="This is a success alert" />
                    <Alert variant="warning" message="This is a warning alert" />
                    <Alert variant="danger" message="This is a danger alert" />
                  </div>
                </div>

                <!-- 带标题的Alert -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">带标题的警告</h4>
                  <div class="space-y-3">
                    <Alert variant="success" title="操作成功" message="您的数据已保存成功！" :closable="true" />
                    <Alert variant="warning" title="注意事项" message="此操作不可撤销，请谨慎操作。" :closable="true" />
                    <Alert variant="danger" title="错误信息" message="网络连接失败，请检查您的网络设置。" :closable="true" />
                  </div>
                </div>

                <!-- 自定义内容 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">自定义内容</h4>
                  <Alert variant="primary" title="系统更新" :closable="true">
                    <div class="text-sm text-blue-700">
                      <p class="mb-2">发现新版本 v2.1.0，包含以下更新：</p>
                      <ul class="list-disc list-inside space-y-1">
                        <li>修复了一些已知问题</li>
                        <li>优化了用户体验</li>
                        <li>增加了新功能模块</li>
                      </ul>
                    </div>
                  </Alert>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                支持多种类型和自定义内容的警告提示组件
              </div>
            </div>
          </div>

          <!-- Modal Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Zap :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Modal</h3>
                    <p class="text-sm text-slate-500">现代化的弹窗组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Modal')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openModalCodeModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-4">
                <!-- 不同尺寸的Modal -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
                  <div class="flex flex-wrap gap-3">
                    <ripple-button text="小尺寸" variant="outline" size="sm" @click="openDemoModal('sm')" />
                    <ripple-button text="中等尺寸" variant="primary" @click="openDemoModal('md')" />
                    <ripple-button text="大尺寸" variant="secondary" @click="openDemoModal('lg')" />
                    <ripple-button text="超大尺寸" variant="success" @click="openDemoModal('xl')" />
                  </div>
                </div>

                <!-- 不同类型的Modal -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同类型</h4>
                  <div class="flex flex-wrap gap-3">
                    <ripple-button text="确认对话框" variant="danger" @click="openConfirmModal" />
                    <ripple-button text="信息弹窗" variant="ghost" @click="openInfoModal" />
                    <ripple-button text="自定义内容" variant="outline" @click="openCustomModal" />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                支持多种尺寸和自定义内容的弹窗组件，使用RippleButton作为操作按钮
              </div>
            </div>
          </div>

          <!-- Dropdown Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <Component :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Dropdown</h3>
                    <p class="text-sm text-slate-500">灵活的下拉菜单组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Dropdown')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openDropdownModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 基础下拉菜单 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">基础下拉菜单</h4>
                  <div class="flex flex-wrap gap-3">
                    <Dropdown 
                      triggerText="Open Menu" 
                      :items="basicDropdownItems"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="操作菜单" 
                      :items="actionDropdownItems"
                      variant="primary"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="更多选项" 
                      :items="moreDropdownItems"
                      variant="outline"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>

                <!-- 不同尺寸 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
                  <div class="flex flex-wrap items-center gap-3">
                    <Dropdown 
                      triggerText="小尺寸" 
                      :items="basicDropdownItems"
                      size="sm"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="中等尺寸" 
                      :items="basicDropdownItems"
                      size="md"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="大尺寸" 
                      :items="basicDropdownItems"
                      size="lg"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>

                <!-- 不同变体 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同变体</h4>
                  <div class="flex flex-wrap gap-3">
                    <Dropdown 
                      triggerText="Default" 
                      :items="basicDropdownItems"
                      variant="default"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="Primary" 
                      :items="basicDropdownItems"
                      variant="primary"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="Outline" 
                      :items="basicDropdownItems"
                      variant="outline"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="Ghost" 
                      :items="basicDropdownItems"
                      variant="ghost"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>

                <!-- 圆角类型 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">圆角类型</h4>
                  <div class="flex flex-wrap gap-3">
                    <Dropdown 
                      triggerText="微微圆角" 
                      :items="basicDropdownItems"
                      variant="primary"
                      :rounded="false"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="椭圆形" 
                      :items="basicDropdownItems"
                      variant="primary"
                      :rounded="true"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="Outline 微微圆" 
                      :items="basicDropdownItems"
                      variant="outline"
                      :rounded="false"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="Outline 椭圆" 
                      :items="basicDropdownItems"
                      variant="outline"
                      :rounded="true"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>

                <!-- 触发模式 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">触发模式</h4>
                  <div class="flex flex-wrap gap-3">
                    <Dropdown 
                      triggerText="点击触发" 
                      :items="basicDropdownItems"
                      variant="primary"
                      trigger="click"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="悬停触发" 
                      :items="basicDropdownItems"
                      variant="secondary"
                      trigger="hover"
                      :hover-delay="200"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="悬停快速" 
                      :items="basicDropdownItems"
                      variant="outline"
                      trigger="hover"
                      :hover-delay="100"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="悬停椭圆" 
                      :items="basicDropdownItems"
                      variant="ghost"
                      trigger="hover"
                      :hover-delay="150"
                      :rounded="true"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>

                <!-- 带图标和功能 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">功能示例</h4>
                  <div class="flex flex-wrap gap-3">
                    <Dropdown 
                      triggerText="用户设置" 
                      :items="userDropdownItems"
                      :prefixIcon="userIcon"
                      @select="handleDropdownSelect"
                    />
                    <Dropdown 
                      triggerText="文件操作" 
                      :items="fileDropdownItems"
                      variant="outline"
                      placement="bottom-end"
                      @select="handleDropdownSelect"
                    />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                支持图标、分割线、快捷键显示和多种位置的下拉菜单组件
              </div>
            </div>
          </div>

          <!-- Drawer Component -->
          <div class="masonry-item bg-white border border-slate-200 rounded-xl overflow-hidden shadow-sm hover:shadow-md transition-shadow">
            <div class="p-6 border-b border-slate-100">
              <div class="flex items-center justify-between">
                <div class="flex items-center space-x-3">
                  <div class="w-10 h-10 bg-slate-100 rounded-lg flex items-center justify-center">
                    <PanelRightOpen :size="20" class="text-slate-600" />
                  </div>
                  <div>
                    <h3 class="text-lg font-semibold text-slate-900">Drawer</h3>
                    <p class="text-sm text-slate-500">四方向拉出的抽屉组件</p>
                  </div>
                </div>
                <div class="flex space-x-2">
                  <button 
                    @click.stop="openParameterModal('Drawer')"
                    class="w-8 h-8 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center justify-center"
                    title="查看参数说明"
                  >
                    <Info :size="16" />
                  </button>
                  <button 
                    @click.stop="openDrawerModal"
                    class="w-8 h-8 bg-slate-900 text-white rounded-lg hover:bg-slate-800 transition-colors flex items-center justify-center"
                    title="查看代码"
                  >
                    <Code2 :size="16" />
                  </button>
                </div>
              </div>
            </div>
            
            <div class="p-6">
              <div class="space-y-6">
                <!-- 不同方向 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同方向</h4>
                  <div class="grid grid-cols-2 gap-3">
                    <ripple-button text="从左侧拉出" variant="outline" @click="openDrawer('left')" />
                    <ripple-button text="从右侧拉出" variant="outline" @click="openDrawer('right')" />
                    <ripple-button text="从顶部拉出" variant="outline" @click="openDrawer('top')" />
                    <ripple-button text="从底部拉出" variant="outline" @click="openDrawer('bottom')" />
                  </div>
                </div>

                <!-- 不同尺寸 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
                  <div class="flex flex-wrap gap-3">
                    <ripple-button text="小尺寸" variant="primary" size="sm" @click="openDrawerWithSize('right', 'sm')" />
                    <ripple-button text="中等尺寸" variant="primary" @click="openDrawerWithSize('right', 'md')" />
                    <ripple-button text="大尺寸" variant="primary" @click="openDrawerWithSize('right', 'lg')" />
                    <ripple-button text="超大尺寸" variant="primary" @click="openDrawerWithSize('right', 'xl')" />
                  </div>
                </div>

                <!-- 带内容的抽屉 -->
                <div>
                  <h4 class="text-sm font-medium text-slate-700 mb-3">功能示例</h4>
                  <div class="flex flex-wrap gap-3">
                    <ripple-button text="设置面板" variant="secondary" @click="openSettingsDrawer" />
                    <ripple-button text="通知中心" variant="ghost" @click="openNotificationDrawer" />
                    <ripple-button text="表单抽屉" variant="success" @click="openFormDrawer" />
                  </div>
                </div>
              </div>
              
              <div class="mt-6 text-xs text-slate-500 text-center">
                支持四个方向滑入滑出，简洁流畅动画，圆角设计，多种尺寸和自定义内容
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900 text-white py-12">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center">
          <div class="flex items-center justify-center space-x-3 mb-4">
            <div class="w-8 h-8 bg-white rounded-lg flex items-center justify-center">
              <Component :size="20" class="text-slate-900" />
            </div>
            <span class="text-xl font-bold">Nice Components</span>
          </div>
          <p class="text-slate-400 mb-6">精美简约的 Vue 3 组件库</p>
          <div class="flex justify-center space-x-6">
            <a href="https://www.nsmao.com" class="text-slate-400 hover:text-white transition-colors" target="_blank">奈斯猫</a>
            <a href="https://github.com/nsmao-com/nice_unocss_components" class="text-slate-400 hover:text-white transition-colors" target="_blank">GitHub</a>
          </div>
        </div>
      </div>
    </footer>

    <!-- Code Modal -->
    <code-modal 
      :visible="isModalVisible" 
      :title="modalTitle" 
      :code-tabs="modalCodeTabs"
      @close="closeModal"
    />

    <!-- Parameter Modal -->
    <parameter-modal 
      :visible="isParameterModalVisible" 
      :title="parameterModalTitle" 
      :parameters="parameterModalData.parameters || []"
      :events="parameterModalData.events || []"
      :slots="parameterModalData.slots || []"
      @close="closeParameterModal"
    />

    <!-- Demo Modals -->
    <Modal
      v-model:visible="modalStates.demo"
      :title="`${demoModalSize.toUpperCase()} 尺寸弹窗`"
      :size="demoModalSize"
      @confirm="handleModalConfirm"
    >
      <p class="text-slate-600 mb-4">
        这是一个 <strong>{{ demoModalSize }}</strong> 尺寸的弹窗示例。
      </p>
      <p class="text-slate-600">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam pulvinar risus non risus hendrerit venenatis. 
        Pellentesque sit amet hendrerit risus, sed porttitor quam.
      </p>
    </Modal>

    <Modal
      v-model:visible="modalStates.confirm"
      title="确认删除"
      cancelText="取消"
      confirmText="删除"
      confirmVariant="danger"
      @confirm="handleDeleteConfirm"
    >
      <p class="text-slate-600">
        确定要删除这个项目吗？此操作无法撤销。
      </p>
    </Modal>

    <Modal
      v-model:visible="modalStates.info"
      title="信息提示"
      :showCancelButton="false"
      confirmText="知道了"
    >
      <p class="text-slate-600 mb-4">
        这是一个信息提示弹窗，只有一个确认按钮。
      </p>
      <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
        <p class="text-blue-800 text-sm">
          💡 提示：这种类型的弹窗通常用于显示重要信息或操作结果。
        </p>
      </div>
    </Modal>

    <Modal
      v-model:visible="modalStates.custom"
      title="自定义操作"
    >
      <div class="space-y-4">
        <p class="text-slate-600">
          这个弹窗展示了如何自定义footer区域的按钮。
        </p>
        <div class="bg-amber-50 border border-amber-200 rounded-lg p-4">
          <p class="text-amber-800 text-sm">
            ⚠️ 请选择您要执行的操作类型。
          </p>
        </div>
      </div>
      
      <template #footer="{ close }">
        <ripple-button text="取消" variant="ghost" @click="close" />
        <ripple-button text="保存草稿" variant="outline" @click="close" />
        <ripple-button text="发布" variant="success" @click="close" />
      </template>
    </Modal>

    <!-- Drawer Components -->
    <!-- 基础抽屉 -->
    <Drawer
      v-model:visible="drawerStates.basic"
      title="基础抽屉"
      :placement="currentDrawerPlacement"
      :size="currentDrawerSize"
    >
      <div class="space-y-4">
        <p class="text-slate-600">这是一个{{ currentDrawerPlacement }}方向的{{ currentDrawerSize }}尺寸抽屉。</p>
        <p class="text-slate-600">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam pulvinar risus non risus hendrerit venenatis.</p>
        <div class="bg-slate-50 border border-slate-200 rounded-lg p-4">
          <p class="text-slate-700 text-sm">
            💡 抽屉组件支持从四个方向拉出，并具有优雅的圆角设计。
          </p>
        </div>
      </div>
    </Drawer>

    <!-- 设置抽屉 -->
    <Drawer
      v-model:visible="drawerStates.settings"
      title="设置中心"
      placement="right"
      size="lg"
      :show-footer="true"
      :show-confirm-button="true"
      confirm-text="保存设置"
      confirm-variant="primary"
    >
      <template #title>
        <div class="flex items-center space-x-2">
          <Settings :size="20" class="text-slate-600" />
          <span>设置中心</span>
        </div>
      </template>

      <div class="space-y-6">
        <div>
          <h4 class="text-sm font-medium text-slate-900 mb-3">通用设置</h4>
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">启用通知</label>
              <checkbox v-model="checkboxStates.primary" variant="primary" size="sm" />
            </div>
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">自动保存</label>
              <checkbox v-model="checkboxStates.success" variant="success" size="sm" />
            </div>
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">深色模式</label>
              <checkbox v-model="checkboxStates.secondary" variant="secondary" size="sm" />
            </div>
          </div>
        </div>

        <div>
          <h4 class="text-sm font-medium text-slate-900 mb-3">语言设置</h4>
          <div class="space-y-2">
            <radio v-model="radioStates.basic" value="option1" label="简体中文" name="language" size="sm" />
            <radio v-model="radioStates.basic" value="option2" label="English" name="language" size="sm" />
            <radio v-model="radioStates.basic" value="option3" label="Français" name="language" size="sm" />
          </div>
        </div>

        <div>
          <h4 class="text-sm font-medium text-slate-900 mb-3">账户信息</h4>
          <div class="space-y-4">
            <input v-model="inputValues.name" label="用户名" placeholder="请输入用户名" />
            <input v-model="inputValues.email2" label="邮箱地址" type="email" placeholder="请输入邮箱" />
          </div>
        </div>
      </div>
    </Drawer>

    <!-- 通知抽屉 -->
    <Drawer
      v-model:visible="drawerStates.notification"
      title="通知中心"
      placement="right"
      size="md"
    >
      <template #title>
        <div class="flex items-center justify-between w-full">
          <div class="flex items-center space-x-2">
            <AlertTriangle :size="20" class="text-amber-500" />
            <span>通知中心</span>
          </div>
          <badge content="3" variant="danger" size="sm" />
        </div>
      </template>

      <div class="space-y-4">
        <Alert
          title="系统更新"
          message="新版本已发布，建议及时更新以获得更好的体验。"
          variant="primary"
          :show-icon="true"
          size="sm"
        />
        
        <Alert
          title="存储空间不足"
          message="您的存储空间即将用完，请及时清理或升级套餐。"
          variant="warning"
          :show-icon="true"
          size="sm"
        />
        
        <Alert
          title="安全提醒"
          message="检测到异常登录，请确认是否为本人操作。"
          variant="danger"
          :show-icon="true"
          size="sm"
        />

        <div class="space-y-3 pt-4 border-t border-slate-200">
          <h4 class="text-sm font-medium text-slate-900">历史通知</h4>
          <div class="space-y-2">
            <div class="p-3 bg-slate-50 rounded-lg">
              <p class="text-sm text-slate-700">欢迎使用 Nice Components</p>
              <p class="text-xs text-slate-500 mt-1">2小时前</p>
            </div>
            <div class="p-3 bg-slate-50 rounded-lg">
              <p class="text-sm text-slate-700">账户验证成功</p>
              <p class="text-xs text-slate-500 mt-1">昨天</p>
            </div>
          </div>
        </div>
      </div>
    </Drawer>

    <!-- 表单抽屉 -->
    <Drawer
      v-model:visible="drawerStates.form"
      title="新建项目"
      placement="right"
      size="lg"
      :show-footer="true"
      :show-confirm-button="true"
      confirm-text="创建项目"
      confirm-variant="success"
    >
      <div class="space-y-6">
        <div>
          <h4 class="text-sm font-medium text-slate-900 mb-4">基本信息</h4>
          <div class="space-y-4">
            <input v-model="inputValues.name" label="项目名称" placeholder="请输入项目名称" />
            <input v-model="inputValues.website" label="项目描述" placeholder="请输入项目描述" />
            
            <div>
              <label class="block text-sm font-medium text-slate-700 mb-2">项目类型</label>
              <div class="space-y-2">
                <radio v-model="radioStates.payment" value="web" label="Web 应用" name="projectType" />
                <radio v-model="radioStates.payment" value="mobile" label="移动应用" name="projectType" />
                <radio v-model="radioStates.payment" value="desktop" label="桌面应用" name="projectType" />
              </div>
            </div>
          </div>
        </div>

        <div>
          <h4 class="text-sm font-medium text-slate-900 mb-4">项目设置</h4>
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">启用TypeScript</label>
              <checkbox v-model="checkboxStates.primary" variant="primary" />
            </div>
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">包含测试文件</label>
              <checkbox v-model="checkboxStates.success" variant="success" />
            </div>
            <div class="flex items-center justify-between">
              <label class="text-sm text-slate-700">自动部署</label>
              <checkbox v-model="checkboxStates.warning" variant="warning" />
            </div>
          </div>
        </div>

        <div class="bg-blue-50 border border-blue-200 rounded-lg p-4">
          <p class="text-blue-800 text-sm">
            💡 创建成功后，您可以在项目管理中查看和编辑项目信息。
          </p>
        </div>
      </div>
    </Drawer>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import SliderTab from './components/SliderTab.vue';
import Carousel from './components/Carousel.vue';
import RippleButton from './components/RippleButton.vue';
import Badge from './components/Badge.vue';
import Checkbox from './components/Checkbox.vue';
import Radio from './components/Radio.vue';
import Input from './components/Input.vue';
import InputOTP from './components/InputOTP.vue';
import Pagination from './components/Pagination.vue';
import Modal from './components/Modal.vue';
import Alert from './components/Alert.vue';
import Dropdown from './components/Dropdown.vue';
import Drawer from './components/Drawer.vue';
import CodeModal from './components/SystemComponents/CodeModal.vue';
import ParameterModal from './components/SystemComponents/ParameterModal.vue';
import { Component, Plus, Code2, Wrench, Globe, HeartHandshake, Image, Info, MousePointer, Download, Save, Trash2, Settings, Heart, Share2, Type, Search, Lock, Zap, AlertTriangle, Menu, PanelRightOpen, ChevronRight } from 'lucide-vue-next';

// Demo state for SliderTab
const activeTab = ref(0);
const tabs = ref([
  { title: '标签一' },
  { title: '标签二' },
  { title: '标签三' },
  { title: '一个比较长的标签' },
]);

// Demo state for Pagination
const paginationCurrentPage = ref(1);

// Demo state for Carousel
const carouselItems = ref([
  { title: '精美设计', description: '现代化的用户界面设计' },
  { title: '高性能', description: '优化的性能和流畅体验' },
  { title: '易于使用', description: '简单直观的操作方式' },
  { title: '响应式', description: '完美适配各种设备' },
]);

// Carousel控制参数
const carouselAutoplay = ref(true);
const carouselAutoplayStart = ref(true);
const carouselPauseOnHover = ref(true);
const carouselInterval = ref(4000);

// Checkbox状态
const checkboxStates = ref({
  default: false,
  primary: true,
  secondary: false,
  success: true,
  warning: false,
  danger: true,
  small: false,
  medium: true,
  large: false,
  roundedPrimary: true,
  roundedSuccess: false,
  roundedDanger: true,
  disabledUnchecked: false,
  disabledChecked: true,
  noLabel1: false,
  noLabel2: true,
  noLabel3: false,
  noLabel4: true,
});

// Radio状态
const radioStates = ref({
  basic: 'option1',
  variants: 'primary',
  sizes: 'md',
  disabled: 'option2', // 设置为option2以显示禁用已选中状态
  noLabel: 'option2',
  payment: 'alipay',
});

// Input状态
const inputValues = ref({
  email1: '',
  name: '',
  email2: '',
  website: '',
  success: 'test@example.com',
  phone: '13812345678',
  errorExample: 'invalid-email',
  disabled: 'Disabled value',
  search: '',
  password: '',
});

// Input OTP状态
const otpValues = ref({
  basic: '',
  short: '',
  long: '',
  small: '',
  large: '',
  numeric: '',
  alphanumeric: '',
  error: '',
  manualError: '',
  disabled: '123456',
  rounded: '',
  password: '',
  roundedPassword: '',
});

// Modal状态
const modalStates = ref({
  demo: false,
  confirm: false,
  info: false,
  custom: false,
});

const demoModalSize = ref('md');

// Drawer状态
const drawerStates = ref({
  basic: false,
  settings: false,
  notification: false,
  form: false,
});

const currentDrawerPlacement = ref('right');
const currentDrawerSize = ref('md');

// Dropdown数据
const basicDropdownItems = ref([
  { label: 'New file', value: 'new' },
  { label: 'Copy link', value: 'copy' },
  { label: 'Edit file', value: 'edit' },
  { divider: true },
  { label: 'Delete file', value: 'delete', variant: 'danger' }
]);

const actionDropdownItems = ref([
  { 
    label: 'Profile', 
    value: 'profile',
    icon: '<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>'
  },
  { 
    label: 'Settings', 
    value: 'settings',
    icon: '<circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="2" fill="none"/><path d="M12 1v6m0 6v6m11-5h-6m-6 0H1m16.5-4a4.5 4.5 0 0 1-9 0 4.5 4.5 0 0 1 9 0Z" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
    shortcut: '⌘,'
  },
  { 
    label: 'Help', 
    value: 'help',
    icon: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3M12 17h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>'
  },
  { divider: true },
  { 
    label: 'Logout', 
    value: 'logout', 
    variant: 'danger',
    icon: '<path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4M16 17l5-5-5-5M21 12H9" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>'
  }
]);

const moreDropdownItems = ref([
  { label: 'View details', value: 'details' },
  { label: 'Share', value: 'share' },
  { label: 'Download', value: 'download' },
  { divider: true },
  { label: 'Archive', value: 'archive' },
  { label: 'Move to trash', value: 'trash', variant: 'danger' }
]);

const userDropdownItems = ref([
  { 
    label: 'My Account', 
    value: 'account',
    icon: '<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>'
  },
  { 
    label: 'Billing', 
    value: 'billing',
    icon: '<rect x="2" y="3" width="20" height="14" rx="2" ry="2" stroke="currentColor" stroke-width="2" fill="none"/><line x1="8" y1="21" x2="16" y2="21" stroke="currentColor" stroke-width="2" stroke-linecap="round"/><line x1="12" y1="17" x2="12" y2="21" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>'
  },
  { 
    label: 'Team', 
    value: 'team',
    icon: '<path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="9" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/><path d="M23 21v-2a4 4 0 0 0-3-3.87M16 3.13a4 4 0 0 1 0 7.75" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>'
  },
  { divider: true },
  { 
    label: 'Support', 
    value: 'support',
    icon: '<circle cx="12" cy="12" r="10" stroke="currentColor" stroke-width="2" fill="none"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3M12 17h.01" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>'
  },
  { 
    label: 'Sign out', 
    value: 'signout', 
    variant: 'danger',
    icon: '<path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4M16 17l5-5-5-5M21 12H9" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>'
  }
]);

const fileDropdownItems = ref([
  { 
    label: 'New file', 
    value: 'new',
    icon: '<path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><polyline points="14,2 14,8 20,8" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
    shortcut: '⌘N'
  },
  { 
    label: 'Copy link', 
    value: 'copy',
    icon: '<path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
    shortcut: '⌘C'
  },
  { 
    label: 'Edit file', 
    value: 'edit',
    icon: '<path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
    shortcut: '⌘E'
  },
  { divider: true },
  { 
    label: 'Delete file', 
    value: 'delete', 
    variant: 'danger',
    icon: '<polyline points="3,6 5,6 21,6" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>',
    shortcut: '⌫'
  }
]);

const userIcon = '<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>';

// Modal state
const isModalVisible = ref(false);
const modalTitle = ref('');
const modalCodeTabs = ref([]);

// Parameter modal state
const isParameterModalVisible = ref(false);
const parameterModalTitle = ref('');
const parameterModalData = ref([]);

// Code for the Modal
const sliderTabUsageCode = `<template>
  <!-- 水平模式 (默认) -->
  <slider-tab :tabs="tabs" v-model="activeTab" :vertical="false" />
  
  <!-- 垂直模式 -->
  <slider-tab :tabs="tabs" v-model="activeTab" :vertical="true" />
</template>

<script setup>
import { ref } from 'vue';
import SliderTab from './components/SliderTab.vue';

const activeTab = ref(0);
const tabs = ref([
  { title: '标签一' },
  { title: '标签二' },
  { title: '标签三' },
  { title: '一个长标签' },
]);
<\/script>`;

const sliderTabSourceCode = `<template>
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
        <div :class="sliderClass" :style="sliderStyle"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch, nextTick } from 'vue';

const props = defineProps({
  tabs: { type: Array, required: true },
  modelValue: { type: Number, required: true },
  vertical: { type: Boolean, default: false }
});

const emit = defineEmits(['update:modelValue']);

const tabsContainer = ref(null);
const tabItems = ref([]);
const sliderWidth = ref(0);
const sliderHeight = ref(0);
const sliderLeft = ref(0);
const sliderTop = ref(0);

const wrapperClass = computed(() => ({
  'w-full flex justify-center py-4': !props.vertical,
  'h-full flex items-center justify-center px-4': props.vertical,
}));

const containerClass = computed(() => 'bg-slate-100 rounded-lg p-1 shadow-sm');

const trackClass = computed(() => ({
  'relative flex gap-0.5': !props.vertical,
  'relative flex flex-col gap-0.5': props.vertical,
}));

const tabItemClass = computed(() => ({
  'relative px-5 py-2.5 cursor-pointer font-medium text-sm text-slate-500 rounded-md transition-all duration-200 z-2 whitespace-nowrap select-none hover:text-slate-600': !props.vertical,
  'relative px-5 py-2.5 cursor-pointer font-medium text-sm text-slate-500 rounded-md transition-all duration-200 z-2 whitespace-nowrap select-none hover:text-slate-600 text-center min-w-24': props.vertical,
}));

const sliderClass = computed(() => ({
  'absolute top-1 bottom-1 bg-white rounded-md transition-all duration-250 z-1 shadow-sm': !props.vertical,
  'absolute left-1 right-1 bg-white rounded-md transition-all duration-250 z-1 shadow-sm': props.vertical,
}));

const sliderStyle = computed(() => {
  if (props.vertical) {
    return {
      height: \`\${sliderHeight.value}px\`,
      transform: \`translateY(\${sliderTop.value}px)\`,
    };
  } else {
    return {
      width: \`\${sliderWidth.value}px\`,
      transform: \`translateX(\${sliderLeft.value}px)\`,
    };
  }
});

const selectTab = (index) => emit('update:modelValue', index);

const updateSlider = () => {
  if (tabItems.value && tabItems.value[props.modelValue]) {
    const activeTab = tabItems.value[props.modelValue];
    if (props.vertical) {
      sliderHeight.value = activeTab.offsetHeight;
      sliderTop.value = activeTab.offsetTop;
    } else {
      sliderWidth.value = activeTab.offsetWidth;
      sliderLeft.value = activeTab.offsetLeft;
    }
  }
};

onMounted(() => nextTick(updateSlider));
watch(() => props.modelValue, () => nextTick(updateSlider));
watch(() => props.tabs, () => nextTick(updateSlider), { deep: true });
watch(() => props.vertical, () => nextTick(updateSlider));
<\/script>`;

// Carousel code examples
const carouselUsageCode = `<template>
  <carousel 
    :items="carouselItems" 
    :interval="4000"
    :autoplay="true"
    :autoplay-start="true"
    :pause-on-hover="true"
    :show-arrows="true"
    :show-indicators="true"
    :show-play-pause="true"
    @change="handleSlideChange"
  />
</template>

<script setup>
import { ref } from 'vue';
import Carousel from './components/Carousel.vue';

const carouselItems = ref([
  { title: '精美设计', description: '现代化的用户界面设计' },
  { title: '高性能', description: '优化的性能和流畅体验' },
  { title: '易于使用', description: '简单直观的操作方式' },
  { title: '响应式', description: '完美适配各种设备' }
]);

const handleSlideChange = (index) => {
  console.log('Current slide:', index);
};
<\/script>`;

const carouselSourceCode = `<template>
  <div class="relative w-full bg-white rounded-xl overflow-hidden shadow-sm border border-slate-200">
    <div 
      class="relative h-64 overflow-hidden"
      @mouseenter="pauseAutoplay"
      @mouseleave="resumeAutoplay"
    >
      <div 
        class="flex transition-transform duration-500 ease-in-out h-full"
        :style="{ transform: \`translateX(-\${currentIndex * 100}%)\` }"
      >
        <div
          v-for="(item, index) in items"
          :key="index"
          class="w-full h-full flex-shrink-0 relative flex items-center justify-center bg-gradient-to-br"
          :class="getSlideClass(index)"
        >
          <div v-if="item.image" class="w-full h-full">
            <img :src="item.image" :alt="item.title" class="w-full h-full object-cover" />
          </div>
          
          <div v-if="item.title || item.description" class="absolute inset-0 bg-black/20 flex items-center justify-center">
            <div class="text-center text-white px-6">
              <h3 v-if="item.title" class="text-2xl font-bold mb-2">{{ item.title }}</h3>
              <p v-if="item.description" class="text-lg opacity-90">{{ item.description }}</p>
            </div>
          </div>
        </div>
      </div>
      
      <button v-if="showArrows" @click="prevSlide" class="absolute left-4 top-1/2 transform -translate-y-1/2 w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition-all duration-200 shadow-lg z-10">
        <ChevronLeft :size="20" />
      </button>
      
      <button v-if="showArrows" @click="nextSlide" class="absolute right-4 top-1/2 transform -translate-y-1/2 w-10 h-10 bg-white/80 hover:bg-white rounded-full flex items-center justify-center transition-all duration-200 shadow-lg z-10">
        <ChevronRight :size="20" />
      </button>
    </div>
    
    <div v-if="showIndicators" class="flex justify-center items-center space-x-2 py-4 bg-slate-50">
      <button v-for="(item, index) in items" :key="index" @click="goToSlide(index)" class="w-2 h-2 rounded-full transition-all duration-300" :class="{ 'bg-slate-900 scale-125': currentIndex === index, 'bg-slate-300 hover:bg-slate-400': currentIndex !== index }"></button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, watch } from 'vue';
import { ChevronLeft, ChevronRight, Play, Pause } from 'lucide-vue-next';

const props = defineProps({
  items: { type: Array, required: true },
  autoplay: { type: Boolean, default: true },
  interval: { type: Number, default: 3000 },
  showArrows: { type: Boolean, default: true },
  showIndicators: { type: Boolean, default: true }
});

const emit = defineEmits(['change']);
const currentIndex = ref(0);
const isPlaying = ref(props.autoplay);
let autoplayTimer = null;

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % props.items.length;
  emit('change', currentIndex.value);
};

const prevSlide = () => {
  currentIndex.value = currentIndex.value === 0 ? props.items.length - 1 : currentIndex.value - 1;
  emit('change', currentIndex.value);
};

const goToSlide = (index) => {
  currentIndex.value = index;
  emit('change', currentIndex.value);
};

const startAutoplay = () => {
  if (props.autoplay && props.items.length > 1) {
    autoplayTimer = setInterval(nextSlide, props.interval);
    isPlaying.value = true;
  }
};

onMounted(() => startAutoplay());
onUnmounted(() => autoplayTimer && clearInterval(autoplayTimer));
<\/script>`;

// RippleButton code examples
const rippleButtonUsageCode = `<template>
  <div class="space-y-4">
    <!-- 不同变体的按钮 -->
    <div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
      <ripple-button text="Primary" variant="primary" @click="handleClick" />
      <ripple-button text="Secondary" variant="secondary" @click="handleClick" />
      <ripple-button text="Outline" variant="outline" @click="handleClick" />
      <ripple-button text="Ghost" variant="ghost" @click="handleClick" />
      <ripple-button text="Danger" variant="danger" @click="handleClick" />
      <ripple-button text="Success" variant="success" @click="handleClick" />
    </div>
    
    <!-- 不同尺寸的按钮 -->
    <div class="flex flex-wrap items-center gap-3">
      <ripple-button text="Small" size="sm" @click="handleClick" />
      <ripple-button text="Medium" size="md" @click="handleClick" />
      <ripple-button text="Large" size="lg" @click="handleClick" />
      <ripple-button text="Extra Large" size="xl" @click="handleClick" />
    </div>
    
    <!-- 特殊按钮 -->
    <div class="space-y-3">
      <ripple-button text="圆形按钮" :rounded="true" @click="handleClick" />
      <ripple-button text="全宽按钮" :full-width="true" @click="handleClick" />
      <ripple-button text="禁用按钮" :disabled="true" @click="handleClick" />
    </div>
    
         <!-- 带图标的按钮 -->
     <div class="flex flex-wrap gap-3">
       <ripple-button text="下载" :icon="Download" variant="outline" @click="handleClick" />
       <ripple-button text="保存" :icon="Save" variant="success" @click="handleClick" />
       <ripple-button text="删除" :icon="Trash2" variant="danger" @click="handleClick" />
       
       <!-- 使用图标插槽 -->
       <ripple-button text="设置" variant="secondary" @click="handleClick">
         <template #icon>
           <Settings :size="16" />
         </template>
       </ripple-button>
       
               <!-- 只有图标的按钮（自动圆形） -->
        <ripple-button variant="ghost" @click="handleClick">
          <template #icon>
            <Heart :size="18" />
          </template>
        </ripple-button>
     </div>
  </div>
</template>

 <script setup>
 import { Download, Save, Trash2, Settings, Heart } from 'lucide-vue-next';
 import RippleButton from './components/RippleButton.vue';

const handleClick = (event) => {
  console.log('Button clicked!', event);
};
<\/script>`;

const rippleButtonSourceCode = `<template>
  <button
    ref="buttonRef"
    :class="buttonClass"
    @click="handleClick"
    @mousedown="handleMouseDown"
    :disabled="disabled"
  >
    <!-- 涟漪容器 -->
    <span class="absolute inset-0 overflow-hidden rounded-inherit">
      <span
        v-for="ripple in ripples"
        :key="ripple.id"
        class="absolute rounded-full bg-white/30 pointer-events-none animate-ripple"
        :style="{
          left: ripple.x + 'px',
          top: ripple.y + 'px',
          width: ripple.size + 'px',
          height: ripple.size + 'px',
          transform: 'translate(-50%, -50%)',
        }"
      ></span>
    </span>

    <!-- 按钮内容 -->
    <span class="relative z-10 flex items-center justify-center space-x-2">
      <component v-if="icon" :is="icon" :size="iconSize" />
      <span v-if="$slots.default"><slot></slot></span>
      <span v-else-if="text">{{ text }}</span>
    </span>
  </button>
</template>

<script setup>
import { ref, computed } from 'vue';

 const props = defineProps({
   text: { type: String, default: '' },
   icon: { type: [String, Object], default: null },
   iconSize: { type: Number, default: 16 },
   variant: { type: String, default: 'primary' },
   size: { type: String, default: 'md' },
   disabled: { type: Boolean, default: false },
   rounded: { type: Boolean, default: false },
   fullWidth: { type: Boolean, default: false },
   customClass: { type: String, default: '' }
 });

 // 判断是否为纯图标按钮，自动设置为圆形
 const isIconOnly = computed(() => {
   return !props.text && !props.$slots?.default && (props.icon || props.$slots?.icon);
 });

const emit = defineEmits(['click']);
const buttonRef = ref(null);
const ripples = ref([]);

// 处理鼠标按下事件，创建涟漪效果
const handleMouseDown = (event) => {
  if (props.disabled) return;
  
  const button = buttonRef.value;
  const rect = button.getBoundingClientRect();
  
  // 计算点击位置相对于按钮的坐标
  const x = event.clientX - rect.left;
  const y = event.clientY - rect.top;
  
  // 计算涟漪的最大尺寸
  const size = Math.max(
    Math.sqrt((x - 0) ** 2 + (y - 0) ** 2),
    Math.sqrt((x - rect.width) ** 2 + (y - 0) ** 2),
    Math.sqrt((x - 0) ** 2 + (y - rect.height) ** 2),
    Math.sqrt((x - rect.width) ** 2 + (y - rect.height) ** 2)
  ) * 2;

  // 创建涟漪对象
  const ripple = { id: Date.now() + Math.random(), x, y, size };
  ripples.value.push(ripple);

  // 动画完成后移除涟漪
  setTimeout(() => {
    const index = ripples.value.findIndex(r => r.id === ripple.id);
    if (index > -1) ripples.value.splice(index, 1);
  }, 600);
};
<\/script>

<style scoped>
@keyframes ripple {
  0% { transform: translate(-50%, -50%) scale(0); opacity: 0.6; }
  100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
}
.animate-ripple { animation: ripple 0.6s ease-out forwards; }
<\/style>`;

// Badge code examples
const badgeUsageCode = `<template>
  <div class="space-y-6">
    <!-- 数字徽章 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">数字徽章</h4>
      <div class="flex items-center gap-4 flex-wrap">
        <div class="relative">
          <div class="w-10 h-10 bg-slate-100 rounded-full flex items-center justify-center">
            <Mail :size="20" class="text-slate-600" />
          </div>
          <badge :content="5" class="absolute -top-1 -right-1" />
        </div>
        <div class="relative">
          <button class="px-4 py-2 bg-blue-500 text-white rounded-lg">
            消息
          </button>
          <badge :content="99" variant="danger" class="absolute -top-2 -right-2" />
        </div>
        <div class="relative">
          <button class="px-4 py-2 bg-green-500 text-white rounded-lg">
            通知
          </button>
          <badge :content="999" :max="99" variant="warning" class="absolute -top-2 -right-2" />
        </div>
      </div>
    </div>

    <!-- 状态点 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">状态点</h4>
      <div class="flex items-center gap-4 flex-wrap">
        <div class="relative">
          <img src="/avatar.jpg" alt="用户头像" class="w-10 h-10 rounded-full bg-slate-200" />
          <badge dot variant="success" class="absolute top-0 right-0" />
        </div>
        <div class="relative">
          <img src="/avatar.jpg" alt="用户头像" class="w-10 h-10 rounded-full bg-slate-200" />
          <badge dot variant="warning" class="absolute top-0 right-0" />
        </div>
      </div>
    </div>

    <!-- 文字徽章 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">文字徽章</h4>
      <div class="flex items-center gap-4 flex-wrap">
        <div class="relative">
          <div class="w-20 h-12 bg-slate-100 rounded-lg flex items-center justify-center">
            <span class="text-xs text-slate-600">产品</span>
          </div>
          <badge content="NEW" variant="danger" size="sm" class="absolute -top-2 -right-2" />
        </div>
        <div class="relative">
          <div class="w-20 h-12 bg-slate-100 rounded-lg flex items-center justify-center">
            <span class="text-xs text-slate-600">热门</span>
          </div>
          <badge content="HOT" variant="warning" size="sm" class="absolute -top-2 -right-2" />
        </div>
      </div>
    </div>

    <!-- 不同样式 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">不同样式</h4>
      <div class="flex items-center gap-3 flex-wrap">
        <badge content="Primary" variant="primary" />
        <badge content="Success" variant="success" />
        <badge content="Warning" variant="warning" />
        <badge content="Danger" variant="danger" />
        <badge content="轮廓" variant="primary" outline />
        <badge content="方形" variant="danger" square />
      </div>
    </div>
  </div>
</template>

<script setup>
import { Mail } from 'lucide-vue-next';
import Badge from './components/Badge.vue';
<\/script>`;

const badgeSourceCode = `<template>
  <span :class="badgeClasses" v-if="shouldShow">
    <slot>{{ displayContent }}</slot>
  </span>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  content: { type: [String, Number], default: '' },
  variant: { type: String, default: 'primary' },
  size: { type: String, default: 'md' },
  dot: { type: Boolean, default: false },
  max: { type: Number, default: 99 },
  showZero: { type: Boolean, default: false },
  color: { type: String, default: '' },
  square: { type: Boolean, default: false },
  outline: { type: Boolean, default: false },
});

// 是否应该显示徽章
const shouldShow = computed(() => {
  if (props.dot) return true;
  if (props.content === 0 || props.content === '0') {
    return props.showZero;
  }
  return props.content !== '' && props.content !== null && props.content !== undefined;
});

// 显示的内容
const displayContent = computed(() => {
  if (props.dot) return '';
  if (typeof props.content === 'number' && props.content > props.max) {
    return \`\${props.max}+\`;
  }
  return props.content;
});

// 基础样式
const baseClasses = computed(() => {
  const classes = [
    'inline-flex items-center justify-center font-medium text-xs leading-none',
    'transition-all duration-200',
  ];

  // 大小
  if (props.dot) {
    switch (props.size) {
      case 'sm': classes.push('w-2 h-2'); break;
      case 'md': classes.push('w-2.5 h-2.5'); break;
      case 'lg': classes.push('w-3 h-3'); break;
    }
  } else {
    switch (props.size) {
      case 'sm': classes.push('min-w-4 h-4 px-1 text-xs'); break;
      case 'md': classes.push('min-w-5 h-5 px-1.5 text-xs'); break;
      case 'lg': classes.push('min-w-6 h-6 px-2 text-sm'); break;
    }
  }

  // 形状
  classes.push(props.square ? 'rounded-sm' : 'rounded-full');
  return classes;
});

// 颜色样式
const colorClasses = computed(() => {
  if (props.color) {
    return props.outline 
      ? \`border-2 text-[\${props.color}] border-[\${props.color}] bg-transparent\`
      : \`bg-[\${props.color}] text-white\`;
  }

  const variants = {
    primary: props.outline ? 'border-2 border-blue-500 text-blue-500 bg-transparent' : 'bg-blue-500 text-white',
    secondary: props.outline ? 'border-2 border-slate-500 text-slate-500 bg-transparent' : 'bg-slate-500 text-white',
    success: props.outline ? 'border-2 border-green-500 text-green-500 bg-transparent' : 'bg-green-500 text-white',
    warning: props.outline ? 'border-2 border-amber-500 text-amber-500 bg-transparent' : 'bg-amber-500 text-white',
    danger: props.outline ? 'border-2 border-red-500 text-red-500 bg-transparent' : 'bg-red-500 text-white',
    info: props.outline ? 'border-2 border-cyan-500 text-cyan-500 bg-transparent' : 'bg-cyan-500 text-white',
  };

  return variants[props.variant] || variants.primary;
});

const badgeClasses = computed(() => [...baseClasses.value, colorClasses.value]);
<\/script>`;

// Checkbox code examples
const checkboxUsageCode = `<template>
  <div class="space-y-6">
    <!-- 基础用法 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">基础用法</h4>
      <div class="flex items-center gap-4">
        <checkbox v-model="checked" label="我同意用户协议" />
        <checkbox v-model="newsletter" label="订阅邮件通知" />
      </div>
    </div>

    <!-- 不同变体 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">不同变体</h4>
      <div class="grid grid-cols-2 gap-4">
        <checkbox v-model="states.primary" variant="primary" label="Primary" />
        <checkbox v-model="states.success" variant="success" label="Success" />
        <checkbox v-model="states.warning" variant="warning" label="Warning" />
        <checkbox v-model="states.danger" variant="danger" label="Danger" />
      </div>
    </div>

    <!-- 不同大小 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">不同大小</h4>
      <div class="flex items-center gap-6">
        <checkbox v-model="sizes.small" size="sm" label="Small" />
        <checkbox v-model="sizes.medium" size="md" label="Medium" />
        <checkbox v-model="sizes.large" size="lg" label="Large" />
      </div>
    </div>

    <!-- 圆形样式 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">圆形样式</h4>
      <div class="flex items-center gap-6">
        <checkbox v-model="rounded.primary" variant="primary" rounded label="圆形 Primary" />
        <checkbox v-model="rounded.success" variant="success" rounded label="圆形 Success" />
      </div>
    </div>

    <!-- 禁用状态 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">禁用状态</h4>
      <div class="flex items-center gap-6">
        <checkbox v-model="disabled.unchecked" disabled label="禁用未选中" />
        <checkbox v-model="disabled.checked" disabled label="禁用已选中" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Checkbox from './components/Checkbox.vue';

const checked = ref(false);
const newsletter = ref(true);

const states = ref({
  primary: true,
  success: false,
  warning: true,
  danger: false,
});

const sizes = ref({
  small: false,
  medium: true,
  large: false,
});

const rounded = ref({
  primary: true,
  success: false,
});

const disabled = ref({
  unchecked: false,
  checked: true,
});
<\/script>`;

const checkboxSourceCode = `<template>
  <label :class="wrapperClass">
    <input
      type="checkbox"
      :checked="modelValue"
      :disabled="disabled"
      :value="value"
      @change="handleChange"
      class="sr-only"
    />
    
    <!-- 复选框容器 -->
    <div :class="checkboxClass">
      <!-- 勾选标记 -->
      <svg
        :class="checkmarkClass"
        viewBox="0 0 16 16"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"
          fill="currentColor"
          :style="checkmarkStyle"
        />
      </svg>
    </div>
    
    <!-- 标签文字 -->
    <span v-if="label || $slots.default" :class="labelClass">
      <slot>{{ label }}</slot>
    </span>
  </label>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const props = defineProps({
  modelValue: { type: Boolean, default: false },
  label: { type: String, default: '' },
  value: { type: [String, Number, Boolean], default: true },
  disabled: { type: Boolean, default: false },
  variant: { type: String, default: 'primary' },
  size: { type: String, default: 'md' },
  rounded: { type: Boolean, default: false },
});

const emit = defineEmits(['update:modelValue', 'change']);

// 动画状态
const animationProgress = ref(0);

// 处理变化事件
const handleChange = (event) => {
  const checked = event.target.checked;
  emit('update:modelValue', checked);
  emit('change', checked, props.value);
};

// 复选框样式
const checkboxClass = computed(() => {
  const classes = [
    'relative flex items-center justify-center border-2 transition-all duration-200',
    'focus-within:ring-2 focus-within:ring-offset-2',
  ];

  // 大小
  switch (props.size) {
    case 'sm': classes.push('w-4 h-4'); break;
    case 'md': classes.push('w-5 h-5'); break;
    case 'lg': classes.push('w-6 h-6'); break;
  }

  // 形状
  classes.push(props.rounded ? 'rounded-full' : 'rounded-md');

  // 颜色状态
  if (props.modelValue) {
    switch (props.variant) {
      case 'primary': classes.push('bg-blue-600 border-blue-600 text-white'); break;
      case 'success': classes.push('bg-green-600 border-green-600 text-white'); break;
      case 'warning': classes.push('bg-amber-600 border-amber-600 text-white'); break;
      case 'danger': classes.push('bg-red-600 border-red-600 text-white'); break;
      default: classes.push('bg-slate-600 border-slate-600 text-white'); break;
    }
  } else {
    classes.push('bg-white border-slate-300 hover:border-slate-400');
  }

  return classes;
});

// 勾选标记动画样式
const checkmarkStyle = computed(() => {
  if (!props.modelValue) {
    return { strokeDasharray: '16', strokeDashoffset: '16', opacity: '0' };
  }
  
  return {
    strokeDasharray: '16',
    strokeDashoffset: \`\${16 - (animationProgress.value * 16)}\`,
    opacity: animationProgress.value > 0.1 ? '1' : '0',
  };
});

// 监听选中状态变化，触发动画
watch(() => props.modelValue, (newVal) => {
  if (newVal) {
    animationProgress.value = 0;
    const startTime = Date.now();
    const duration = 300;

    const animate = () => {
      const elapsed = Date.now() - startTime;
      const progress = Math.min(elapsed / duration, 1);
      animationProgress.value = 1 - Math.pow(1 - progress, 3);
      
      if (progress < 1) requestAnimationFrame(animate);
    };
    
    requestAnimationFrame(animate);
  } else {
    animationProgress.value = 0;
  }
}, { immediate: true });
<\/script>

<style scoped>
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
<\/style>`;

// Radio code examples
const radioUsageCode = `<template>
  <div class="space-y-6">
    <!-- 基础单选组 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">基础选项</h4>
      <div class="space-y-2">
        <radio v-model="selected" name="basic" value="option1" label="选项 1" />
        <radio v-model="selected" name="basic" value="option2" label="选项 2" />
        <radio v-model="selected" name="basic" value="option3" label="选项 3" />
      </div>
      <div class="text-xs text-slate-500">当前选择: {{ selected || '无' }}</div>
    </div>

    <!-- 不同变体 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">不同变体</h4>
      <div class="grid grid-cols-2 gap-4">
        <radio v-model="variants" name="variants" value="primary" variant="primary" label="Primary" />
        <radio v-model="variants" name="variants" value="success" variant="success" label="Success" />
        <radio v-model="variants" name="variants" value="warning" variant="warning" label="Warning" />
        <radio v-model="variants" name="variants" value="danger" variant="danger" label="Danger" />
      </div>
    </div>

    <!-- 不同大小 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">不同大小</h4>
      <div class="flex items-center gap-6">
        <radio v-model="sizes" name="sizes" value="sm" size="sm" label="Small" />
        <radio v-model="sizes" name="sizes" value="md" size="md" label="Medium" />
        <radio v-model="sizes" name="sizes" value="lg" size="lg" label="Large" />
      </div>
    </div>

    <!-- 禁用状态 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">禁用状态</h4>
      <div class="space-y-2">
        <radio v-model="disabled" name="disabled" value="option1" disabled label="禁用未选中" />
        <radio v-model="disabled" name="disabled" value="option2" disabled label="禁用已选中" />
        <radio v-model="disabled" name="disabled" value="option3" label="正常选项" />
      </div>
    </div>

    <!-- 实际应用示例 -->
    <div class="space-y-3">
      <h4 class="text-sm font-medium text-slate-700">付款方式选择</h4>
      <div class="space-y-2">
        <radio v-model="payment" name="payment" value="alipay" variant="primary" label="支付宝" />
        <radio v-model="payment" name="payment" value="wechat" variant="success" label="微信支付" />
        <radio v-model="payment" name="payment" value="unionpay" variant="warning" label="银联支付" />
        <radio v-model="payment" name="payment" value="card" variant="secondary" label="银行卡" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Radio from './components/Radio.vue';

const selected = ref('option1');
const variants = ref('primary');
const sizes = ref('md');
const disabled = ref('option2'); // 设置为option2以显示禁用已选中状态
const payment = ref('alipay');
<\/script>`;

const radioSourceCode = `<template>
  <label :class="wrapperClass">
    <input
      type="radio"
      :checked="isChecked"
      :disabled="disabled"
      :value="value"
      :name="name"
      @change="handleChange"
      class="sr-only"
    />
    
    <!-- 单选框容器 -->
    <div :class="radioContainerClass" :style="containerDynamicStyle">
      <!-- 选中圆点 -->
      <div
        v-if="isChecked"
        :class="dotClass"
        :style="dotStyle"
      ></div>
    </div>
    
    <!-- 标签文字 -->
    <span v-if="label || $slots.default" :class="labelClass">
      <slot>{{ label }}</slot>
    </span>
  </label>
</template>

<script setup>
import { computed, ref, watch } from 'vue';

const props = defineProps({
  modelValue: { type: [String, Number, Boolean], default: null },
  label: { type: String, default: '' },
  value: { type: [String, Number, Boolean], required: true },
  name: { type: String, default: '' },
  disabled: { type: Boolean, default: false },
  variant: { type: String, default: 'primary' },
  size: { type: String, default: 'md' },
});

const emit = defineEmits(['update:modelValue', 'change']);

// 动画状态
const backgroundScale = ref(0);
const dotScale = ref(0);

// 是否选中
const isChecked = computed(() => props.modelValue === props.value);

// 处理变化事件
const handleChange = (event) => {
  if (event.target.checked) {
    emit('update:modelValue', props.value);
    emit('change', props.value);
  }
};

// 单选框容器样式
const radioContainerClass = computed(() => {
  const classes = [
    'relative flex items-center justify-center border-2 rounded-full overflow-hidden',
    'focus-within:ring-2 focus-within:ring-offset-2',
    'transition-colors duration-300 ease-out',
  ];

  // 大小
  switch (props.size) {
    case 'sm': classes.push('w-4 h-4'); break;
    case 'md': classes.push('w-5 h-5'); break;
    case 'lg': classes.push('w-6 h-6'); break;
  }

  // 边框颜色
  if (isChecked.value) {
    switch (props.variant) {
      case 'primary': classes.push('border-blue-600 focus-within:ring-blue-500'); break;
      case 'success': classes.push('border-green-600 focus-within:ring-green-500'); break;
      case 'warning': classes.push('border-amber-600 focus-within:ring-amber-500'); break;
      case 'danger': classes.push('border-red-600 focus-within:ring-red-500'); break;
      default: classes.push('border-slate-600 focus-within:ring-slate-500'); break;
    }
  } else {
    classes.push('border-slate-300 hover:border-slate-400 focus-within:ring-blue-500');
  }

  return classes;
});

// 容器动态样式 - 背景色动画
const containerDynamicStyle = computed(() => {
  const getBackgroundColor = () => {
    if (!isChecked.value) return 'white';
    
    const alpha = backgroundScale.value;
    switch (props.variant) {
      case 'primary': return \`rgba(37, 99, 235, \${alpha})\`;
      case 'success': return \`rgba(22, 163, 74, \${alpha})\`;
      case 'warning': return \`rgba(217, 119, 6, \${alpha})\`;
      case 'danger': return \`rgba(220, 38, 38, \${alpha})\`;
      default: return \`rgba(71, 85, 105, \${alpha})\`;
    }
  };

  return { backgroundColor: getBackgroundColor() };
});

// 圆点样式
const dotClass = computed(() => {
  const classes = ['absolute rounded-full bg-white transition-all duration-300 ease-out'];
  
  switch (props.size) {
    case 'sm': classes.push('w-1.5 h-1.5'); break;
    case 'md': classes.push('w-2 h-2'); break;
    case 'lg': classes.push('w-2.5 h-2.5'); break;
  }

  return classes;
});

// 圆点动画样式
const dotStyle = computed(() => {
  return {
    transform: \`scale(\${dotScale.value})\`,
    transformOrigin: 'center',
  };
});

// 监听选中状态变化，触发动画
watch(() => isChecked.value, (newVal) => {
  if (newVal) {
    // 选中动画：先背景填充，然后圆点出现
    backgroundScale.value = 0;
    dotScale.value = 0;
    
    const startTime = Date.now();
    const backgroundDuration = 200;
    const dotDelay = 100;
    const dotDuration = 200;

    const animate = () => {
      const elapsed = Date.now() - startTime;
      
      // 背景填充动画
      if (elapsed <= backgroundDuration) {
        const progress = elapsed / backgroundDuration;
        backgroundScale.value = progress < 0.5 
          ? 2 * progress * progress 
          : 1 - Math.pow(-2 * progress + 2, 2) / 2;
      } else {
        backgroundScale.value = 1;
      }
      
      // 圆点动画
      if (elapsed >= dotDelay) {
        const dotElapsed = elapsed - dotDelay;
        if (dotElapsed <= dotDuration) {
          const progress = dotElapsed / dotDuration;
          dotScale.value = progress < 0.5 
            ? 2 * progress * progress 
            : 1 - Math.pow(-2 * progress + 2, 2) / 2;
        } else {
          dotScale.value = 1;
        }
      }
      
      if (elapsed < backgroundDuration + dotDuration) {
        requestAnimationFrame(animate);
      }
    };
    
    requestAnimationFrame(animate);
  } else {
    // 取消选中动画
    const startTime = Date.now();
    const duration = 150;

    const animate = () => {
      const elapsed = Date.now() - startTime;
      const progress = Math.min(elapsed / duration, 1);
      
      const scale = 1 - (progress < 0.5 
        ? 2 * progress * progress 
        : 1 - Math.pow(-2 * progress + 2, 2) / 2);
      
      backgroundScale.value = scale;
      dotScale.value = scale;
      
      if (progress < 1) {
        requestAnimationFrame(animate);
      } else {
        backgroundScale.value = 0;
        dotScale.value = 0;
      }
    };
    
    requestAnimationFrame(animate);
  }
}, { immediate: true });
<\/script>

<style scoped>
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
<\/style>`;

// Input code examples
const inputUsageCode = `<template>
  <div class="space-y-6">
    <!-- 固定标签模式 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">固定标签模式</h4>
      <div class="space-y-4">
        <Input 
          v-model="email1" 
          label="Email" 
          description="请输入您的邮箱地址"
        />
        <Input 
          v-model="name" 
          label="用户名" 
          description="请输入6-20位字符的用户名"
          variant="primary"
        />
      </div>
    </div>
    
    <!-- 浮动标签模式 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">浮动标签模式</h4>
      <div class="space-y-4">
        <Input 
          v-model="email2" 
          label="Email" 
          placeholder="请输入邮箱地址"
        />
        <Input 
          v-model="website" 
          label="网站地址" 
          placeholder="请输入网站URL"
          variant="success"
        />
      </div>
    </div>

    <!-- 验证功能 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">验证功能</h4>
      <div class="space-y-4">
        <Input 
          v-model="success" 
          label="Email验证" 
          :validationType="'email'"
          :showValidationIcon="true"
          placeholder="输入邮箱地址"
          variant="success"
        />
        <Input 
          v-model="phone" 
          label="电话验证" 
          :validationType="'phone'"
          :showValidationIcon="true"
          placeholder="输入电话号码"
          variant="warning"
        />
      </div>
    </div>

    <!-- 状态示例 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">状态示例</h4>
      <div class="space-y-4">
        <Input 
          v-model="errorExample" 
          label="错误状态" 
          errorMessage="邮箱格式不正确，请重新输入"
          placeholder="invalid-email"
        />
        <Input 
          v-model="disabled" 
          label="禁用状态" 
          :disabled="true"
          placeholder="Disabled input"
        />
      </div>
    </div>

    <!-- 功能增强 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">功能增强</h4>
      <div class="space-y-4">
        <Input 
          v-model="search" 
          label="搜索" 
          :prefixIcon="Search"
          :clearable="true"
          placeholder="搜索内容..."
        />
        <Input 
          v-model="password" 
          label="密码验证" 
          type="password"
          :suffixIcon="Lock"
          :validationType="'password'"
          :showValidationIcon="true"
          placeholder="请输入密码"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Search, Lock } from 'lucide-vue-next';
import Input from './components/Input.vue';

const email1 = ref('');
const name = ref('');
const email2 = ref('');
const website = ref('');
const success = ref('test@example.com');
const phone = ref('13812345678');
const errorExample = ref('invalid-email');
const disabled = ref('Disabled value');
const search = ref('');
const password = ref('');
<\/script>`;

const inputSourceCode = `<template>
  <div :class="groupClass">
    <!-- 固定标签模式 - label在输入框外部 -->
    <label 
      v-if="label && description"
      :for="inputId" 
      :class="fixedLabelClass"
    >
      {{ label }}
    </label>
    
    <!-- 输入框包装器 -->
    <div :class="inputWrapperClass" @click="focusInput">
      <!-- 浮动标签 - 只在无description时显示 -->
      <label 
        v-if="label && !description"
        :for="inputId" 
        :class="floatingLabelClass"
      >
        {{ label }}
      </label>
      
      <!-- 内部包装器 -->
      <div :class="innerWrapperClass">
        <!-- 前置图标 -->
        <div v-if="prefixIcon" :class="prefixIconClass">
          <component :is="prefixIcon" :size="iconSize" />
        </div>
        
        <!-- 输入框 -->
        <input
          :id="inputId"
          :type="type"
          :value="modelValue"
          :placeholder="computedPlaceholder"
          :disabled="disabled"
          :readonly="readonly"
          :class="inputClass"
          @input="handleInput"
          @focus="handleFocus"
          @blur="handleBlur"
          @change="handleChange"
          ref="inputRef"
        />
        
        <!-- 验证图标 -->
        <div v-if="shouldShowValidationIcon" :class="validationIconClass">
          <Check v-if="validationStatus === true" :size="iconSize" />
          <AlertCircle v-else-if="validationStatus === false" :size="iconSize" />
        </div>
        
        <!-- 后置图标 -->
        <div v-if="suffixIcon" :class="suffixIconClass">
          <component :is="suffixIcon" :size="iconSize" />
        </div>
        
        <!-- 清除按钮 -->
        <button
          v-if="clearable && modelValue && !disabled"
          @click="handleClear"
          :class="clearButtonClass"
          type="button"
        >
          <X :size="14" />
        </button>
      </div>
    </div>
    
    <!-- 帮助文本或错误信息 -->
    <div v-if="helpText || computedErrorMessage" :class="messageClass">
      <p v-if="computedErrorMessage" class="text-red-600 text-sm">{{ computedErrorMessage }}</p>
      <p v-else-if="helpText" class="text-slate-500 text-sm">{{ helpText }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, nextTick } from 'vue';
import { X, Check, AlertCircle } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  modelValue: { type: [String, Number], default: '' },
  label: { type: String, default: '' },
  description: { type: String, default: '' },
  placeholder: { type: String, default: '' },
  type: { type: String, default: 'text' },
  
  // 状态
  disabled: { type: Boolean, default: false },
  readonly: { type: Boolean, default: false },
  error: { type: Boolean, default: false },
  
  // 样式
  variant: { type: String, default: 'default' },
  size: { type: String, default: 'md' },
  
  // 验证
  validationType: { type: String, default: '' },
  showValidationIcon: { type: Boolean, default: true },
  
  // 功能
  clearable: { type: Boolean, default: false },
  prefixIcon: { type: [String, Object, Function], default: null },
  suffixIcon: { type: [String, Object, Function], default: null },
  
  // 消息
  helpText: { type: String, default: '' },
  errorMessage: { type: String, default: '' },
});

const emit = defineEmits(['update:modelValue', 'focus', 'blur', 'change', 'clear']);

// 状态
const isFocused = ref(false);
const inputRef = ref(null);

// 验证规则
const validationRules = {
  email: {
    validate: (value) => {
      if (!value) return null;
      const emailRegex = /^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$/;
      return emailRegex.test(value);
    },
    errorMessage: '请输入有效的邮箱地址'
  },
  phone: {
    validate: (value) => {
      if (!value) return null;
      const phoneRegex = /^[+]?[\\d\\s\\-\\(\\)]+$/;
      return phoneRegex.test(value) && value.replace(/\\D/g, '').length >= 10;
    },
    errorMessage: '请输入有效的电话号码'
  },
  password: {
    validate: (value) => {
      if (!value) return null;
      return value.length >= 6 && /[a-zA-Z]/.test(value) && /\\d/.test(value);
    },
    errorMessage: '密码至少6位，需包含字母和数字'
  },
};

// 验证状态
const validationStatus = computed(() => {
  if (!props.validationType) return null;
  const rule = validationRules[props.validationType];
  return rule ? rule.validate(props.modelValue) : null;
});

// 是否显示验证图标
const shouldShowValidationIcon = computed(() => {
  return props.showValidationIcon && props.validationType && props.modelValue && props.modelValue.length > 0;
});

// 计算错误信息
const computedErrorMessage = computed(() => {
  if (props.errorMessage) return props.errorMessage;
  if (props.validationType && validationStatus.value === false) {
    const rule = validationRules[props.validationType];
    return rule ? rule.errorMessage : '';
  }
  return '';
});

// 是否有值或聚焦
const hasValueOrFocus = computed(() => {
  return isFocused.value || (props.modelValue !== '' && props.modelValue !== null && props.modelValue !== undefined);
});

// 计算占位符
const computedPlaceholder = computed(() => {
  if (props.description) return props.description;
  if (props.label && !props.description) {
    return hasValueOrFocus.value ? props.placeholder : '';
  }
  return props.placeholder;
});

// 浮动标签样式
const floatingLabelClass = computed(() => {
  const baseClasses = [
    'absolute z-10 pointer-events-none origin-top-left',
    'block cursor-text duration-200 ease-out transition-all',
    'pr-2 max-w-full overflow-hidden top-1/2 transform select-none',
  ];

  baseClasses.push(props.prefixIcon ? 'left-11' : 'left-3');

  if (hasValueOrFocus.value) {
    let textColor = 'text-slate-600';
    
    if (props.error || computedErrorMessage.value) {
      textColor = 'text-red-600';
    } else if (isFocused.value) {
      switch (props.variant) {
        case 'primary': textColor = 'text-blue-600'; break;
        case 'success': textColor = 'text-green-600'; break;
        case 'warning': textColor = 'text-amber-600'; break;
        case 'danger': textColor = 'text-red-600'; break;
        default: textColor = 'text-slate-600'; break;
      }
    }
    
    baseClasses.push(
      textColor,
      'pointer-events-auto',
      'text-xs',
      'scale-100',
      '-translate-y-4',
    );
    
    if (props.prefixIcon) {
      baseClasses.push('-translate-x-8');
    }
  } else {
    baseClasses.push(
      'text-slate-500',
      'text-sm',
      'scale-100',
      '-translate-y-1/2',
    );
  }

  return baseClasses;
});

// 事件处理
const handleInput = (event) => emit('update:modelValue', event.target.value);
const handleFocus = (event) => { isFocused.value = true; emit('focus', event); };
const handleBlur = (event) => { isFocused.value = false; emit('blur', event); };
const handleChange = (event) => emit('change', event);
const handleClear = () => { emit('update:modelValue', ''); emit('clear'); nextTick(() => inputRef.value?.focus()); };
const focusInput = () => { if (!props.disabled) inputRef.value?.focus(); };
<\/script>`;

// Input OTP code examples
const inputOTPUsageCode = `<template>
  <div class="space-y-8">
    <!-- 基础使用 -->
    <div class="text-center">
      <InputOTP 
        v-model="otpValue" 
        label="请输入验证码"
        helpText="6位数字验证码"
        @complete="handleOTPComplete"
      />
      <div class="mt-2 text-sm text-slate-600">
        当前值: {{ otpValue || '无' }}
      </div>
    </div>

    <!-- 不同长度 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="shortOTP" 
          label="4位验证码"
          :length="4"
          variant="primary"
        />
      </div>
      <div class="text-center">
        <InputOTP 
          v-model="longOTP" 
          label="8位验证码"
          :length="8"
          variant="success"
        />
      </div>
    </div>

    <!-- 不同尺寸 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="smallOTP" 
          label="小尺寸"
          size="sm"
          :length="4"
          variant="warning"
        />
      </div>
      <div class="text-center">
        <InputOTP 
          v-model="largeOTP" 
          label="大尺寸"
          size="lg"
          :length="5"
          variant="danger"
        />
      </div>
    </div>

    <!-- 不同输入类型 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="numericOTP" 
          label="仅数字"
          type="numeric"
          :length="6"
          helpText="只能输入数字0-9"
        />
      </div>
      <div class="text-center">
        <InputOTP 
          v-model="alphanumericOTP" 
          label="字母数字"
          type="alphanumeric"
          :length="6"
          variant="primary"
          helpText="可输入字母和数字"
        />
      </div>
    </div>

    <!-- 自动错误检测 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="autoErrorOTP" 
          label="自动错误检测"
          helpText="输入部分内容后失焦，会自动显示错误提示"
        />
      </div>
      <div class="text-center">
        <InputOTP 
          v-model="manualErrorOTP" 
          label="手动错误状态"
          :error="true"
          errorMessage="验证码错误，请重新输入"
        />
      </div>
    </div>

    <!-- 禁用状态 -->
    <div class="text-center">
      <InputOTP 
        v-model="disabledOTP" 
        label="禁用状态"
        :disabled="true"
        helpText="此输入框已禁用"
      />
    </div>

    <!-- 自动聚焦 -->
    <div class="text-center">
      <InputOTP 
        v-model="autoFocusOTP" 
        label="自动聚焦"
        :autoFocus="true"
        variant="primary"
        helpText="页面加载时自动聚焦"
      />
    </div>

    <!-- 圆角样式 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="roundedOTP" 
          label="圆形输入框"
          :rounded="true"
          variant="primary"
          helpText="使用rounded参数设置为圆形"
        />
      </div>
    </div>

    <!-- 密码隐藏 -->
    <div class="space-y-4">
      <div class="text-center">
        <InputOTP 
          v-model="passwordOTP" 
          label="密码模式"
          :password="true"
          variant="success"
          helpText="输入内容会显示为圆点"
        />
      </div>
      <div class="text-center">
        <InputOTP 
          v-model="roundedPasswordOTP" 
          label="圆形密码模式"
          :rounded="true"
          :password="true"
          variant="warning"
          helpText="圆形输入框 + 密码隐藏"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import InputOTP from './components/InputOTP.vue';

// 状态数据
const otpValue = ref('');
const shortOTP = ref('');
const longOTP = ref('');
const smallOTP = ref('');
const largeOTP = ref('');
const numericOTP = ref('');
const alphanumericOTP = ref('');
const autoErrorOTP = ref('');
const manualErrorOTP = ref('');
const disabledOTP = ref('123456');
const autoFocusOTP = ref('');
const roundedOTP = ref('');
const passwordOTP = ref('');
const roundedPasswordOTP = ref('');

// 事件处理
const handleOTPComplete = (value) => {
  console.log('OTP 完成输入:', value);
  // 这里可以进行验证码验证
};
<\/script>`;

const inputOTPSourceCode = `<template>
  <div :class="groupClass">
    <!-- 标签 -->
    <label v-if="label" :class="labelClass">{{ label }}</label>
    
    <!-- OTP输入框组 -->
    <div :class="otpContainerClass">
      <input
        v-for="(digit, index) in digits"
        :key="index"
        :ref="setInputRef"
        :value="password && digit ? '•' : digit"
        :disabled="disabled"
        :class="inputClass(index)"
        type="text"
        inputmode="numeric"
        maxlength="1"
        autocomplete="one-time-code"
        @input="handleInput(index, $event)"
        @keydown="handleKeyDown(index, $event)"
        @focus="handleFocus(index)"
        @blur="handleBlur(index)"
        @paste="handlePaste($event)"
      />
    </div>
    
    <!-- 帮助文本或错误信息 -->
    <div v-if="helpText || errorMessage" :class="messageClass">
      <p v-if="errorMessage" class="text-red-600 text-sm">{{ errorMessage }}</p>
      <p v-else-if="helpText" class="text-slate-500 text-sm">{{ helpText }}</p>
    </div>
  </div>
</template>

<script setup>
import { computed, ref, watch, nextTick } from 'vue';

const props = defineProps({
  modelValue: { type: String, default: '' },
  label: { type: String, default: '' },
  length: { type: Number, default: 6, validator: (value) => value >= 1 && value <= 10 },
  disabled: { type: Boolean, default: false },
  error: { type: Boolean, default: false },
  variant: { type: String, default: 'default' },
  size: { type: String, default: 'md' },
  type: { type: String, default: 'numeric' },
  helpText: { type: String, default: '' },
  errorMessage: { type: String, default: '' },
  autoFocus: { type: Boolean, default: false },
  secure: { type: Boolean, default: false },
  rounded: { type: Boolean, default: false },
  password: { type: Boolean, default: false },
});

const emit = defineEmits(['update:modelValue', 'complete', 'focus', 'blur', 'change']);

// 状态
const digits = ref(Array(props.length).fill(''));
const inputRefs = ref([]);
const focusedIndex = ref(-1);

// 输入验证
const isValidInput = (value) => {
  switch (props.type) {
    case 'numeric': return /^\\d$/.test(value);
    case 'text': return /^[a-zA-Z]$/.test(value);
    case 'alphanumeric': return /^[a-zA-Z0-9]$/.test(value);
    default: return true;
  }
};

// 监听modelValue变化，同步到digits
watch(() => props.modelValue, (newValue) => {
  const valueArray = (newValue || '').split('').slice(0, props.length);
  digits.value = [...valueArray, ...Array(props.length - valueArray.length).fill('')];
}, { immediate: true });

// 监听digits变化，发出事件
watch(digits, (newDigits) => {
  const value = newDigits.join('');
  emit('update:modelValue', value);
  emit('change', value);
  
  if (value.length === props.length && !value.includes('')) {
    emit('complete', value);
  }
}, { deep: true });

// 样式计算
const inputClass = computed(() => (index) => {
  const baseClasses = [
    'flex items-center justify-center text-center font-medium',
    'border border-slate-200',
    'transition-all duration-200 ease-out',
    'focus:outline-none focus:ring-0',
    'bg-white',
  ];
  
  // 圆角样式
  if (props.rounded) {
    baseClasses.push('rounded-full');
  } else {
    baseClasses.push('rounded-lg');
  }
  
  // 尺寸
  switch (props.size) {
    case 'sm': baseClasses.push('w-8 h-8 text-sm'); break;
    case 'lg': baseClasses.push('w-14 h-14 text-lg'); break;
    default: baseClasses.push('w-12 h-12 text-base');
  }
  
  // 状态样式
  if (props.disabled) {
    baseClasses.push('bg-slate-100 cursor-not-allowed text-slate-400');
  } else if (props.error) {
    baseClasses.push('border-red-300 bg-red-50 text-red-900');
  } else if (digits.value[index] && focusedIndex.value !== index) {
    baseClasses.push('border-slate-300 bg-slate-50 text-slate-900');
  } else if (focusedIndex.value === index) {
    baseClasses.push('border-blue-500 bg-blue-50 ring-4 ring-blue-100');
  } else {
    baseClasses.push('border-slate-200 text-slate-900 hover:border-slate-300');
  }
  
  return baseClasses;
});

// 事件处理
const handleInput = (index, event) => {
  if (props.disabled) return;
  
  const value = event.target.value;
  const lastChar = value.slice(-1);
  
  if (lastChar === '' || isValidInput(lastChar)) {
    digits.value[index] = lastChar;
    
    if (lastChar && index < props.length - 1) {
      nextTick(() => {
        inputRefs.value[index + 1]?.focus();
      });
    }
  } else {
    event.target.value = digits.value[index];
  }
};

const handleKeyDown = (index, event) => {
  if (props.disabled) return;
  
  switch (event.key) {
    case 'Backspace':
      if (!digits.value[index] && index > 0) {
        digits.value[index - 1] = '';
        nextTick(() => inputRefs.value[index - 1]?.focus());
      } else {
        digits.value[index] = '';
      }
      break;
    case 'ArrowLeft':
      event.preventDefault();
      if (index > 0) inputRefs.value[index - 1]?.focus();
      break;
    case 'ArrowRight':
      event.preventDefault();
      if (index < props.length - 1) inputRefs.value[index + 1]?.focus();
      break;
  }
};

const handleFocus = (index) => {
  focusedIndex.value = index;
  emit('focus', index);
};

const handleBlur = (index) => {
  focusedIndex.value = -1;
  emit('blur', index);
};

const handlePaste = (event) => {
  if (props.disabled) return;
  
  event.preventDefault();
  const pastedData = event.clipboardData.getData('text');
  const validChars = pastedData.split('').filter(char => isValidInput(char));
  const startIndex = Math.max(0, focusedIndex.value);
  
  for (let i = 0; i < validChars.length && startIndex + i < props.length; i++) {
    digits.value[startIndex + i] = validChars[i];
  }
  
  const nextIndex = Math.min(startIndex + validChars.length, props.length - 1);
  nextTick(() => inputRefs.value[nextIndex]?.focus());
};
<\/script>`;

// Pagination code examples
const paginationUsageCode = `<template>
  <div class="space-y-8 p-6">
    <!-- 基础分页 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">基础分页</h4>
      <pagination 
        v-model:currentPage="currentPage"
        :totalPages="20"
        @change="handlePageChange"
      />
      <div class="text-xs text-slate-500 mt-2">当前页: {{ currentPage }}/20</div>
    </div>
    
    <!-- 不同尺寸 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
      <div class="space-y-3">
        <div>
          <span class="text-xs text-slate-500 mr-2">小尺寸:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="10"
            size="sm"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">中等尺寸:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="10"
            size="md"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">大尺寸:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="10"
            size="lg"
          />
        </div>
      </div>
    </div>
    
    <!-- 不同变体 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">不同变体</h4>
      <div class="space-y-3">
        <div>
          <span class="text-xs text-slate-500 mr-2">默认样式:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            variant="default"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">主要样式:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            variant="primary"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">极简样式:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            variant="minimal"
          />
        </div>
      </div>
    </div>
    
    <!-- 功能选项 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">功能选项</h4>
      <div class="space-y-3">
        <div>
          <span class="text-xs text-slate-500 mr-2">无箭头:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            :showArrows="false"
          />
        </div>

        <div>
          <span class="text-xs text-slate-500 mr-2">紧凑模式:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            :compact="true"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">圆形样式:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            :rounded="true"
          />
        </div>
        <div>
          <span class="text-xs text-slate-500 mr-2">紧凑+圆形:</span>
          <pagination 
            v-model:currentPage="currentPage"
            :totalPages="8"
            :compact="true"
            :rounded="true"
          />
        </div>
      </div>
    </div>
    
    <!-- 禁用状态 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">禁用状态</h4>
      <pagination 
        v-model:currentPage="currentPage"
        :totalPages="8"
        :disabled="true"
      />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Pagination from './components/Pagination.vue';

const currentPage = ref(1);

const handlePageChange = (page) => {
  console.log('页面切换到:', page);
};
<\/script>`;

const paginationSourceCode = `<template>
  <div :class="paginationClass">
    <!-- 上一页按钮 -->
    <button
      v-if="showArrows"
      :disabled="currentPage === 1"
      @click="goToPage(currentPage - 1)"
      :class="arrowButtonClass(false)"
      aria-label="上一页"
    >
      <ChevronLeft :size="16" />
    </button>

    <!-- 页码列表 -->
    <div :class="pagesContainerClass">
      <!-- 第一页 -->
      <button
        v-if="showFirstPage"
        @click="goToPage(1)"
        :class="pageButtonClass(1)"
      >
        1
      </button>

      <!-- 前省略号 -->
      <span v-if="showStartEllipsis" :class="ellipsisClass">...</span>

      <!-- 中间页码 -->
      <button
        v-for="page in visiblePages"
        :key="page"
        @click="goToPage(page)"
        :class="pageButtonClass(page)"
      >
        {{ page }}
      </button>

      <!-- 后省略号 -->
      <span v-if="showEndEllipsis" :class="ellipsisClass">...</span>

      <!-- 最后一页 -->
      <button
        v-if="showLastPage"
        @click="goToPage(totalPages)"
        :class="pageButtonClass(totalPages)"
      >
        {{ totalPages }}
      </button>
    </div>

    <!-- 下一页按钮 -->
    <button
      v-if="showArrows"
      :disabled="currentPage === totalPages"
      @click="goToPage(currentPage + 1)"
      :class="arrowButtonClass(true)"
      aria-label="下一页"
    >
      <ChevronRight :size="16" />
    </button>
  </div>
</template>

<script setup>
import { computed } from 'vue';
import { ChevronLeft, ChevronRight } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  currentPage: {
    type: Number,
    default: 1,
  },
  totalPages: {
    type: Number,
    required: true,
    validator: (value) => value > 0,
  },
  
  // 显示控制
  showArrows: {
    type: Boolean,
    default: true,
  },
  maxVisiblePages: {
    type: Number,
    default: 7,
    validator: (value) => value >= 3 && value % 2 === 1,
  },
  
  // 样式
  variant: {
    type: String,
    default: 'default',
    validator: (value) => ['default', 'primary', 'minimal'].includes(value),
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['sm', 'md', 'lg'].includes(value),
  },
  
  // 功能选项
  compact: {
    type: Boolean,
    default: false,
  },
  rounded: {
    type: Boolean,
    default: false,
  },
  
  // 禁用状态
  disabled: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(['update:currentPage', 'change']);

// 计算可见页码逻辑...
// 样式计算逻辑...
// 事件处理逻辑...

const goToPage = (page) => {
  if (props.disabled || page === props.currentPage || page < 1 || page > props.totalPages) {
    return;
  }
  
  emit('update:currentPage', page);
  emit('change', page);
};
<\/script>`;

// Modal code examples
const modalUsageCode = `<template>
  <div>
    <!-- 触发按钮 -->
    <RippleButton text="打开弹窗" @click="showModal = true" />
    
    <!-- 基础Modal -->
    <Modal
      v-model:visible="showModal"
      title="Modal Title"
      content="Lorem ipsum dolor sit amet, consectetur adipiscing elit."
      @confirm="handleConfirm"
      @close="handleClose"
    />
    
    <!-- 自定义尺寸 -->
    <Modal
      v-model:visible="showLargeModal"
      title="大尺寸弹窗"
      size="lg"
      @confirm="handleConfirm"
    >
      <p>这是一个大尺寸的弹窗内容...</p>
    </Modal>
    
    <!-- 确认对话框 -->
    <Modal
      v-model:visible="showConfirmModal"
      title="确认删除"
      cancelText="取消"
      confirmText="删除"
      confirmVariant="danger"
      @confirm="handleDelete"
    >
      <p>确定要删除这个项目吗？此操作无法撤销。</p>
    </Modal>
    
    <!-- 自定义footer -->
    <Modal
      v-model:visible="showCustomModal"
      title="自定义操作"
    >
      <p>自定义内容...</p>
      
      <template #footer="{ close }">
        <RippleButton text="取消" variant="ghost" @click="close" />
        <RippleButton text="保存草稿" variant="outline" @click="saveDraft" />
        <RippleButton text="发布" variant="success" @click="publish" />
      </template>
    </Modal>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Modal from './components/Modal.vue';
import RippleButton from './components/RippleButton.vue';

const showModal = ref(false);
const showLargeModal = ref(false);
const showConfirmModal = ref(false);
const showCustomModal = ref(false);

const handleConfirm = () => {
  console.log('确认操作');
  showModal.value = false;
};

const handleClose = () => {
  console.log('关闭弹窗');
};

const handleDelete = () => {
  console.log('执行删除');
  showConfirmModal.value = false;
};

const saveDraft = () => {
  console.log('保存草稿');
  showCustomModal.value = false;
};

const publish = () => {
  console.log('发布内容');
  showCustomModal.value = false;
};
<\/script>`;

const modalSourceCode = `<template>
  <Teleport to="body">
    <Transition
      name="modal"
      enter-active-class="duration-300"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="duration-200"
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
          enter-active-class="duration-300"
          enter-from-class="scale-95 opacity-0"
          enter-to-class="scale-100 opacity-100"
          leave-active-class="duration-200"
          leave-from-class="scale-100 opacity-100"
          leave-to-class="scale-95 opacity-0"
        >
          <div
            v-if="visible"
            :class="modalClass"
            @click.stop
          >
            <!-- Header -->
            <div class="flex items-center justify-between p-6 border-b border-slate-200">
              <h3 class="text-lg font-semibold text-slate-900">
                <slot name="title">{{ title }}</slot>
              </h3>
              <button
                @click="handleClose"
                class="text-slate-400 hover:text-slate-600 transition-colors p-1 rounded-md hover:bg-slate-100"
              >
                <X :size="20" />
              </button>
            </div>
            
            <!-- Body -->
            <div :class="bodyClass">
              <slot>
                <p class="text-slate-600">{{ content }}</p>
              </slot>
            </div>
            
            <!-- Footer -->
            <div v-if="showFooter" class="flex justify-end space-x-3 p-6 border-t border-slate-200 bg-slate-50">
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
import { computed, watch, nextTick, onUnmounted } from 'vue';
import { X } from 'lucide-vue-next';
import RippleButton from './RippleButton.vue';

const props = defineProps({
  visible: { type: Boolean, default: false },
  title: { type: String, default: 'Modal Title' },
  content: { type: String, default: '' },
  size: { type: String, default: 'md' },
  showFooter: { type: Boolean, default: true },
  showCancelButton: { type: Boolean, default: true },
  showConfirmButton: { type: Boolean, default: true },
  cancelText: { type: String, default: 'Close' },
  confirmText: { type: String, default: 'Action' },
  confirmVariant: { type: String, default: 'primary' },
  closeOnBackdrop: { type: Boolean, default: true },
  closeOnEsc: { type: Boolean, default: true },
});

const emit = defineEmits(['update:visible', 'close', 'confirm']);

// Modal容器样式
const modalClass = computed(() => {
  const baseClasses = [
    'relative bg-white rounded-xl shadow-2xl border border-slate-200',
    'max-h-[90vh] overflow-hidden flex flex-col',
  ];

  const sizeClasses = {
    sm: 'w-full max-w-md',
    md: 'w-full max-w-lg',
    lg: 'w-full max-w-2xl',
    xl: 'w-full max-w-4xl',
    full: 'w-[95vw] h-[95vh]',
  };

  return [...baseClasses, sizeClasses[props.size]].join(' ');
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
    nextTick(() => {
      document.addEventListener('keydown', handleEscKey);
      document.body.style.overflow = 'hidden';
    });
  } else {
    document.removeEventListener('keydown', handleEscKey);
    document.body.style.overflow = '';
  }
});

onUnmounted(() => {
  document.removeEventListener('keydown', handleEscKey);
  document.body.style.overflow = '';
});
<\/script>

<style scoped>
.modal-enter-active, .modal-leave-active {
  transition: opacity 0.3s ease;
}
.modal-enter-from, .modal-leave-to {
  opacity: 0;
}
.modal-content-enter-active, .modal-content-leave-active {
  transition: all 0.3s ease;
}
.modal-content-enter-from, .modal-content-leave-to {
  opacity: 0;
  transform: scale(0.95);
}
<\/style>`;

// Modal control functions
const openSliderTabModal = () => {
  modalTitle.value = 'Slider Tab 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: sliderTabUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: sliderTabSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openCarouselModal = () => {
  modalTitle.value = 'Carousel 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: carouselUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: carouselSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openRippleButtonModal = () => {
  modalTitle.value = 'RippleButton 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: rippleButtonUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: rippleButtonSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openBadgeModal = () => {
  modalTitle.value = 'Badge 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: badgeUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: badgeSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openCheckboxModal = () => {
  modalTitle.value = 'Checkbox 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: checkboxUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: checkboxSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openRadioModal = () => {
  modalTitle.value = 'Radio 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: radioUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: radioSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openInputModal = () => {
  modalTitle.value = 'Input 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: inputUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: inputSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openInputOTPModal = () => {
  modalTitle.value = 'Input OTP 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: inputOTPUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: inputOTPSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openPaginationModal = () => {
  modalTitle.value = 'Pagination 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: paginationUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: paginationSourceCode,
    }
  ];
  isModalVisible.value = true;
};

const openModalCodeModal = () => {
  modalTitle.value = 'Modal 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: modalUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: modalSourceCode,
    }
  ];
  isModalVisible.value = true;
};

// Alert code examples
const alertUsageCode = `<template>
  <div class="space-y-4">
    <!-- 基础用法 -->
    <div class="space-y-3">
      <Alert variant="default" message="This is a default alert" />
      <Alert variant="primary" message="This is a primary alert" />
      <Alert variant="secondary" message="This is a secondary alert" />
      <Alert variant="success" message="This is a success alert" />
      <Alert variant="warning" message="This is a warning alert" />
      <Alert variant="danger" message="This is a danger alert" />
    </div>

    <!-- 带标题和关闭按钮 -->
    <div class="space-y-3">
      <Alert 
        variant="success" 
        title="操作成功" 
        message="您的数据已保存成功！" 
        :closable="true" 
        @close="handleAlertClose"
      />
      <Alert 
        variant="warning" 
        title="注意事项" 
        message="此操作不可撤销，请谨慎操作。" 
        :closable="true" 
      />
    </div>

    <!-- 自定义内容 -->
    <Alert variant="primary" title="系统更新" :closable="true">
      <div>
        <p class="mb-2">发现新版本 v2.1.0，包含以下更新：</p>
        <ul class="list-disc list-inside space-y-1">
          <li>修复了一些已知问题</li>
          <li>优化了用户体验</li>
          <li>增加了新功能模块</li>
        </ul>
      </div>
    </Alert>

    <!-- 无图标 -->
    <Alert 
      variant="info" 
      message="这是一个无图标的提示信息" 
      :show-icon="false" 
    />

    <!-- 自定义图标 -->
    <Alert 
      variant="warning" 
      title="自定义图标" 
      message="使用自定义图标的警告提示" 
      :icon="CustomIcon" 
    />
  </div>
</template>

<script setup>
import { Bell } from 'lucide-vue-next';
import Alert from './components/Alert.vue';

const CustomIcon = Bell;

const handleAlertClose = () => {
  console.log('Alert关闭');
};
<\/script>`;

const alertSourceCode = `<template>
  <div :class="alertClass" v-if="visible">
    <!-- 图标 -->
    <div v-if="showIcon" :class="iconContainerClass">
      <component v-if="currentIcon" :is="currentIcon" :size="14" class="text-white" />
    </div>
    
    <!-- 内容 -->
    <div class="flex-1">
      <div v-if="title" :class="titleClass">{{ title }}</div>
      <div :class="messageClass">
        <slot>{{ message }}</slot>
      </div>
    </div>
    
    <!-- 关闭按钮 -->
    <div v-if="closable" class="ml-3">
      <button
        @click="handleClose"
        :class="closeButtonClass"
      >
        <X :size="16" />
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import { X, Info, CheckCircle, AlertTriangle, AlertCircle, HelpCircle } from 'lucide-vue-next';

const props = defineProps({
  // 基础属性
  title: { type: String, default: '' },
  message: { type: String, default: '' },
  variant: { type: String, default: 'default' }, // default, primary, secondary, success, warning, danger
  
  // 显示控制
  visible: { type: Boolean, default: true },
  closable: { type: Boolean, default: false },
  
  // 图标
  icon: { type: [String, Object, Function], default: null },
  showIcon: { type: Boolean, default: true },
  iconSize: { type: Number, default: 20 },
  
  // 样式
  size: { type: String, default: 'md' }, // sm, md, lg
  rounded: { type: Boolean, default: false },
});

const emit = defineEmits(['close']);

// 默认图标映射
const defaultIcons = {
  default: Info,
  primary: Info,
  secondary: HelpCircle,
  success: CheckCircle,
  warning: AlertTriangle,
  danger: AlertCircle,
};

// 当前图标
const currentIcon = computed(() => {
  if (!props.showIcon) return null;
  return props.icon || defaultIcons[props.variant] || defaultIcons.default;
});

// Alert容器样式
const alertClass = computed(() => {
  const baseClasses = [
    'flex items-center px-4 py-3 transition-all duration-200',
  ];

  // 圆角
  baseClasses.push(props.rounded ? 'rounded-full' : 'rounded-lg');

  // 变体颜色
  switch (props.variant) {
    case 'default':
      baseClasses.push('bg-gray-50');
      break;
    case 'primary':
      baseClasses.push('bg-blue-50');
      break;
    case 'secondary':
      baseClasses.push('bg-purple-50');
      break;
    case 'success':
      baseClasses.push('bg-green-50');
      break;
    case 'warning':
      baseClasses.push('bg-yellow-50');
      break;
    case 'danger':
      baseClasses.push('bg-red-50');
      break;
  }

  return baseClasses;
});

// 图标容器样式 - 圆形背景
const iconContainerClass = computed(() => {
  const baseClasses = [
    'flex-shrink-0 mr-3 w-5 h-5 rounded-full flex items-center justify-center'
  ];

  // 图标背景颜色
  switch (props.variant) {
    case 'default': baseClasses.push('bg-gray-700'); break;
    case 'primary': baseClasses.push('bg-blue-600'); break;
    case 'secondary': baseClasses.push('bg-purple-600'); break;
    case 'success': baseClasses.push('bg-green-600'); break;
    case 'warning': baseClasses.push('bg-yellow-600'); break;
    case 'danger': baseClasses.push('bg-red-600'); break;
  }

  return baseClasses;
});

// 处理关闭
const handleClose = () => {
  emit('close');
};
<\/script>`;

const openAlertModal = () => {
  modalTitle.value = 'Alert 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: alertUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: alertSourceCode,
    }
  ];
  isModalVisible.value = true;
};

// Dropdown code examples
const dropdownUsageCode = `<template>
  <div class="space-y-6">
    <!-- 基础下拉菜单 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">基础下拉菜单</h4>
      <div class="flex flex-wrap gap-3">
        <Dropdown 
          triggerText="Open Menu" 
          :items="basicItems"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="操作菜单" 
          :items="actionItems"
          variant="primary"
          @select="handleSelect"
        />
      </div>
    </div>

    <!-- 不同尺寸 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">不同尺寸</h4>
      <div class="flex flex-wrap items-center gap-3">
        <Dropdown 
          triggerText="小尺寸" 
          :items="basicItems"
          size="sm"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="中等尺寸" 
          :items="basicItems"
          size="md"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="大尺寸" 
          :items="basicItems"
          size="lg"
          @select="handleSelect"
        />
      </div>
    </div>

    <!-- 不同变体 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">不同变体</h4>
      <div class="flex flex-wrap gap-3">
        <Dropdown 
          triggerText="Default" 
          :items="basicItems"
          variant="default"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="Primary" 
          :items="basicItems"
          variant="primary"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="Outline" 
          :items="basicItems"
          variant="outline"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="Ghost" 
          :items="basicItems"
          variant="ghost"
          @select="handleSelect"
        />
      </div>
    </div>

    <!-- 圆角类型 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">圆角类型</h4>
      <div class="flex flex-wrap gap-3">
        <Dropdown 
          triggerText="微微圆角" 
          :items="basicItems"
          variant="primary"
          :rounded="false"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="椭圆形" 
          :items="basicItems"
          variant="primary"
          :rounded="true"
          @select="handleSelect"
        />
      </div>
    </div>

    <!-- 触发模式 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">触发模式</h4>
      <div class="flex flex-wrap gap-3">
        <Dropdown 
          triggerText="点击触发" 
          :items="basicItems"
          variant="primary"
          trigger="click"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="悬停触发" 
          :items="basicItems"
          variant="secondary"
          trigger="hover"
          :hover-delay="200"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="悬停快速" 
          :items="basicItems"
          variant="outline"
          trigger="hover"
          :hover-delay="100"
          @select="handleSelect"
        />
      </div>
    </div>

    <!-- 带图标和功能 -->
    <div>
      <h4 class="text-sm font-medium text-slate-700 mb-3">功能示例</h4>
      <div class="flex flex-wrap gap-3">
        <Dropdown 
          triggerText="用户设置" 
          :items="userItems"
          :prefixIcon="userIcon"
          @select="handleSelect"
        />
        <Dropdown 
          triggerText="文件操作" 
          :items="fileItems"
          variant="outline"
          placement="bottom-end"
          trigger="hover"
          :hover-delay="150"
          @select="handleSelect"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Dropdown from './components/Dropdown.vue';

const basicItems = ref([
  { label: 'New file', value: 'new' },
  { label: 'Copy link', value: 'copy' },
  { label: 'Edit file', value: 'edit' },
  { divider: true },
  { label: 'Delete file', value: 'delete', variant: 'danger' }
]);

const actionItems = ref([
  { 
    label: 'Profile', 
    value: 'profile',
    icon: '<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>'
  },
  { 
    label: 'Settings', 
    value: 'settings',
    icon: '<circle cx="12" cy="12" r="3" stroke="currentColor" stroke-width="2" fill="none"/>',
    shortcut: '⌘,'
  },
  { divider: true },
  { 
    label: 'Logout', 
    value: 'logout', 
    variant: 'danger',
    icon: '<path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4M16 17l5-5-5-5M21 12H9" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>'
  }
]);

const userIcon = '<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/><circle cx="12" cy="7" r="4" stroke="currentColor" stroke-width="2" fill="none"/>';

const handleSelect = (item) => {
  console.log('Selected:', item);
};
<\/script>`;

const dropdownSourceCode = `<template>
  <div class="relative inline-block text-left" ref="dropdownRef">
    <!-- 触发按钮 -->
    <button
      @click="toggleDropdown"
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
        <div class="py-1" role="none">
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
  
  // 图标
  prefixIcon: { type: String, default: null },
  
  // 下拉菜单位置
  placement: { type: String, default: 'bottom-start' }, // bottom-start, bottom-end, top-start, top-end
  
  // 其他选项
  closeOnClick: { type: Boolean, default: true },
  autoClose: { type: Boolean, default: true },
});

const emit = defineEmits(['select', 'open', 'close']);

// 状态
const isOpen = ref(false);
const dropdownRef = ref(null);

// 切换下拉菜单
const toggleDropdown = () => {
  if (props.disabled) return;
  
  if (isOpen.value) {
    closeDropdown();
  } else {
    openDropdown();
  }
};

// 处理项目点击
const handleItemClick = (item) => {
  if (item.disabled) return;
  
  emit('select', item);
  
  if (props.closeOnClick) {
    closeDropdown();
  }
};

// 点击外部关闭
const handleClickOutside = (event) => {
  if (props.autoClose && dropdownRef.value && !dropdownRef.value.contains(event.target)) {
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
});
<\/script>`;

const openDropdownModal = () => {
  modalTitle.value = 'Dropdown 组件';
  modalCodeTabs.value = [
    {
      title: '用法示例',
      language: 'xml',
      code: dropdownUsageCode,
    },
    {
      title: '组件源码',
      language: 'xml',
      code: dropdownSourceCode,
    }
  ];
  isModalVisible.value = true;
};

// Dropdown事件处理
const handleDropdownSelect = (item) => {
  console.log('Dropdown选择:', item);
};

// Input OTP事件处理
const handleOTPComplete = (type, value) => {
  console.log(`${type} OTP 完成输入:`, value);
};

// Modal演示方法
const openDemoModal = (size) => {
  demoModalSize.value = size;
  modalStates.value.demo = true;
};

const openConfirmModal = () => {
  modalStates.value.confirm = true;
};

const openInfoModal = () => {
  modalStates.value.info = true;
};

const openCustomModal = () => {
  modalStates.value.custom = true;
};

const handleModalConfirm = () => {
  console.log('Modal确认操作');
  modalStates.value.demo = false;
};

const handleDeleteConfirm = () => {
  console.log('执行删除操作');
  modalStates.value.confirm = false;
};

const closeModal = () => {
  isModalVisible.value = false;
};

// 参数说明弹窗方法
const openParameterModal = (component) => {
  parameterModalTitle.value = component;
  
  if (component === 'Pagination') {
    parameterModalData.value = {
      parameters: [
        { name: 'currentPage', type: 'Number', default: '1', required: false, description: '当前页码，支持 v-model' },
        { name: 'totalPages', type: 'Number', default: '', required: true, description: '总页数，必须大于 0' },
        { name: 'showArrows', type: 'Boolean', default: 'true', required: false, description: '是否显示左右箭头按钮' },
        { name: 'maxVisiblePages', type: 'Number', default: '7', required: false, description: '最大可见页码数量，必须是奇数且至少为 3' },
        { name: 'variant', type: 'String', default: "'default'", required: false, description: '分页样式变体：default, primary, minimal' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '分页大小：sm, md, lg' },

        { name: 'compact', type: 'Boolean', default: 'false', required: false, description: '是否启用紧凑模式，去除页码间距' },
        { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '是否使用圆形样式，false为微微圆角，true为圆形' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用整个分页组件' },
      ],
      events: [
        { name: 'update:currentPage', params: 'page: Number', description: '当页码改变时触发' },
        { name: 'change', params: 'page: Number', description: '当页码改变时触发（同update:currentPage）' },
      ],
      slots: []
    };
  } else if (component === 'SliderTab') {
    parameterModalData.value = {
      parameters: [
        { name: 'tabs', type: 'Array', required: true, description: '标签数据，可以是字符串数组或对象数组' },
        { name: 'modelValue', type: 'Number', required: true, description: '当前选中的标签索引，支持 v-model' },
        { name: 'vertical', type: 'Boolean', default: 'false', required: false, description: '是否为垂直布局模式' },
      ],
      events: [
        { name: 'update:modelValue', params: 'index: Number', description: '当选中标签改变时触发' },
      ],
      slots: []
    };
  } else if (component === 'Carousel') {
    parameterModalData.value = {
      parameters: [
        { name: 'items', type: 'Array', required: true, description: '轮播项数据数组' },
        { name: 'interval', type: 'Number', default: '4000', required: false, description: '自动播放间隔时间（毫秒）' },
        { name: 'autoplay', type: 'Boolean', default: 'true', required: false, description: '是否启用自动播放' },
        { name: 'autoplayStart', type: 'Boolean', default: 'true', required: false, description: '组件加载时是否立即开始自动播放' },
        { name: 'pauseOnHover', type: 'Boolean', default: 'true', required: false, description: '鼠标悬停时是否暂停播放' },
        { name: 'vertical', type: 'Boolean', default: 'false', required: false, description: '是否为垂直轮播模式' },
        { name: 'showArrows', type: 'Boolean', default: 'true', required: false, description: '是否显示左右箭头' },
        { name: 'showIndicators', type: 'Boolean', default: 'true', required: false, description: '是否显示指示器' },
        { name: 'showPlayPause', type: 'Boolean', default: 'true', required: false, description: '是否显示播放/暂停按钮' },
      ],
      events: [
        { name: 'change', params: 'index: Number', description: '当轮播项改变时触发' },
        { name: 'play', params: '', description: '开始播放时触发' },
        { name: 'pause', params: '', description: '暂停播放时触发' },
      ],
      slots: [
        { name: 'default', scope: '{ item, index }', description: '自定义轮播项内容' },
      ]
    };
  } else if (component === 'RippleButton') {
    parameterModalData.value = {
      parameters: [
        { name: 'text', type: 'String', default: "''", required: false, description: '按钮显示的文字' },
        { name: 'icon', type: 'String | Object | Function', default: 'null', required: false, description: '按钮图标组件' },
        { name: 'iconSize', type: 'Number', default: '16', required: false, description: '图标大小' },
        { name: 'variant', type: 'String', default: "'primary'", required: false, description: '按钮变体：primary, secondary, outline, ghost, danger, success' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '按钮尺寸：sm, md, lg, xl' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用按钮' },
        { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '是否为圆形按钮' },
        { name: 'fullWidth', type: 'Boolean', default: 'false', required: false, description: '是否为全宽按钮' },
        { name: 'customClass', type: 'String', default: "''", required: false, description: '自定义CSS类名' },
      ],
      events: [
        { name: 'click', params: 'event: MouseEvent', description: '按钮被点击时触发' },
      ],
      slots: [
        { name: 'default', scope: '', description: '按钮内容插槽，优先级高于text属性' },
        { name: 'icon', scope: '', description: '图标插槽，优先级高于icon属性' },
      ]
    };
  } else if (component === 'Badge') {
    parameterModalData.value = {
      parameters: [
        { name: 'content', type: 'String | Number', default: "''", required: false, description: '徽章显示的内容' },
        { name: 'variant', type: 'String', default: "'primary'", required: false, description: '徽章变体：primary, secondary, success, warning, danger, info' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '徽章大小：sm, md, lg' },
        { name: 'dot', type: 'Boolean', default: 'false', required: false, description: '是否显示为点状徽章' },
        { name: 'max', type: 'Number', default: '99', required: false, description: '最大数字，超过显示 99+' },
        { name: 'showZero', type: 'Boolean', default: 'false', required: false, description: '是否显示 0' },
        { name: 'color', type: 'String', default: "''", required: false, description: '自定义颜色' },
        { name: 'square', type: 'Boolean', default: 'false', required: false, description: '是否为方形徽章' },
        { name: 'outline', type: 'Boolean', default: 'false', required: false, description: '是否为轮廓样式' },
      ],
      events: [],
      slots: [
        { name: 'default', scope: '', description: '自定义徽章内容，优先级高于content属性' },
      ]
    };
  } else if (component === 'Checkbox') {
    parameterModalData.value = {
      parameters: [
        { name: 'modelValue', type: 'Boolean', default: 'false', required: false, description: '复选框的选中状态，支持 v-model' },
        { name: 'label', type: 'String', default: "''", required: false, description: '复选框的标签文字' },
        { name: 'value', type: 'String | Number | Boolean', default: 'true', required: false, description: '复选框的值' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用复选框' },
        { name: 'variant', type: 'String', default: "'primary'", required: false, description: '颜色变体：default, primary, secondary, success, warning, danger' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '复选框大小：sm, md, lg' },
        { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '是否为圆形复选框' },
      ],
      events: [
        { name: 'update:modelValue', params: 'checked: Boolean', description: '当复选框状态改变时触发' },
        { name: 'change', params: 'checked: Boolean, value: any', description: '当复选框状态改变时触发，包含复选框的值' },
      ],
      slots: [
        { name: 'default', scope: '', description: '自定义标签内容，优先级高于label属性' },
      ]
    };
  } else if (component === 'Radio') {
    parameterModalData.value = {
      parameters: [
        { name: 'modelValue', type: 'String | Number | Boolean', default: 'null', required: false, description: '单选框的选中值，支持 v-model' },
        { name: 'label', type: 'String', default: "''", required: false, description: '单选框的标签文字' },
        { name: 'value', type: 'String | Number | Boolean', default: '', required: true, description: '单选框的值，必需参数' },
        { name: 'name', type: 'String', default: "''", required: false, description: '单选框的分组名称，相同name的单选框属于同一组' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用单选框' },
        { name: 'variant', type: 'String', default: "'primary'", required: false, description: '颜色变体：default, primary, secondary, success, warning, danger' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '单选框大小：sm, md, lg' },
      ],
      events: [
        { name: 'update:modelValue', params: 'value: any', description: '当单选框状态改变时触发' },
        { name: 'change', params: 'value: any', description: '当单选框状态改变时触发，包含单选框的值' },
      ],
      slots: [
        { name: 'default', scope: '', description: '自定义标签内容，优先级高于label属性' },
      ]
    };
  } else if (component === 'Input') {
    parameterModalData.value = {
      parameters: [
        { name: 'modelValue', type: 'String | Number', default: "''", required: false, description: '输入框的值，支持 v-model' },
        { name: 'label', type: 'String', default: "''", required: false, description: '输入框的标签文字' },
        { name: 'description', type: 'String', default: "''", required: false, description: '描述文字，有description时为固定标签模式，无description时为浮动标签模式' },
        { name: 'placeholder', type: 'String', default: "''", required: false, description: '占位符文字' },
        { name: 'type', type: 'String', default: "'text'", required: false, description: '输入框类型：text, password, email, number, tel, url等' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用输入框' },
        { name: 'readonly', type: 'Boolean', default: 'false', required: false, description: '是否只读' },
        { name: 'error', type: 'Boolean', default: 'false', required: false, description: '是否显示错误状态' },
        { name: 'variant', type: 'String', default: "'default'", required: false, description: '颜色变体：default, primary, secondary, success, warning, danger' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '输入框大小：sm, md, lg' },
        { name: 'validationType', type: 'String', default: "''", required: false, description: '验证类型：email, phone, url, number, password' },
        { name: 'showValidationIcon', type: 'Boolean', default: 'true', required: false, description: '是否显示验证图标' },
        { name: 'clearable', type: 'Boolean', default: 'false', required: false, description: '是否显示清除按钮' },
        { name: 'prefixIcon', type: 'Component', default: 'null', required: false, description: '前置图标组件' },
        { name: 'suffixIcon', type: 'Component', default: 'null', required: false, description: '后置图标组件' },
        { name: 'helpText', type: 'String', default: "''", required: false, description: '帮助文本' },
        { name: 'errorMessage', type: 'String', default: "''", required: false, description: '自定义错误信息，验证失败时会自动显示默认错误信息' },
      ],
      events: [
        { name: 'update:modelValue', params: 'value: String | Number', description: '当输入框值改变时触发' },
        { name: 'focus', params: 'event: FocusEvent', description: '当输入框获得焦点时触发' },
        { name: 'blur', params: 'event: FocusEvent', description: '当输入框失去焦点时触发' },
        { name: 'change', params: 'event: Event', description: '当输入框值改变并失去焦点时触发' },
        { name: 'clear', params: '', description: '当点击清除按钮时触发' },
      ],
      slots: []
    };
  } else if (component === 'InputOTP') {
    parameterModalData.value = {
      parameters: [
        { name: 'modelValue', type: 'String', default: "''", required: false, description: '输入的验证码值，支持 v-model' },
        { name: 'label', type: 'String', default: "''", required: false, description: '组件的标签文字' },
        { name: 'length', type: 'Number', default: '6', required: false, description: '验证码位数，1-10之间' },
                 { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用所有输入框' },
         { name: 'error', type: 'Boolean', default: 'false', required: false, description: '手动设置错误状态，组件会自动在失焦且输入不完整时显示错误' },
         { name: 'variant', type: 'String', default: "'default'", required: false, description: '颜色变体：default, primary, success, warning, danger' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '输入框尺寸：sm, md, lg' },
        { name: 'type', type: 'String', default: "'numeric'", required: false, description: '输入类型：numeric, text, alphanumeric' },
        { name: 'helpText', type: 'String', default: "''", required: false, description: '帮助文本' },
        { name: 'errorMessage', type: 'String', default: "''", required: false, description: '错误提示信息' },
                 { name: 'autoFocus', type: 'Boolean', default: 'false', required: false, description: '是否自动聚焦到第一个输入框' },
         { name: 'secure', type: 'Boolean', default: 'false', required: false, description: '是否为安全模式，隐藏输入内容' },
         { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '是否为圆形输入框，false为微微圆角，true为圆形' },
         { name: 'password', type: 'Boolean', default: 'false', required: false, description: '是否为密码模式，隐藏输入字符显示为圆点' },
      ],
      events: [
        { name: 'update:modelValue', params: 'value: String', description: '当验证码值改变时触发' },
        { name: 'complete', params: 'value: String', description: '当所有位数都输入完成时触发' },
        { name: 'focus', params: 'index: Number', description: '当某个输入框获得焦点时触发' },
        { name: 'blur', params: 'index: Number', description: '当某个输入框失去焦点时触发' },
        { name: 'change', params: 'value: String', description: '当验证码值改变时触发（同update:modelValue）' },
      ],
      slots: []
    };
  } else if (component === 'Modal') {
    parameterModalData.value = {
      parameters: [
        { name: 'visible', type: 'Boolean', default: 'false', required: false, description: '弹窗的显示状态，支持 v-model' },
        { name: 'title', type: 'String', default: "'Modal Title'", required: false, description: '弹窗标题' },
        { name: 'content', type: 'String', default: "''", required: false, description: '弹窗内容文本' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '弹窗尺寸：sm, md, lg, xl, full' },
        { name: 'showFooter', type: 'Boolean', default: 'true', required: false, description: '是否显示底部操作区域' },
        { name: 'showCancelButton', type: 'Boolean', default: 'true', required: false, description: '是否显示取消按钮' },
        { name: 'showConfirmButton', type: 'Boolean', default: 'true', required: false, description: '是否显示确认按钮' },
        { name: 'cancelText', type: 'String', default: "'Close'", required: false, description: '取消按钮文本' },
        { name: 'confirmText', type: 'String', default: "'Action'", required: false, description: '确认按钮文本' },
        { name: 'confirmVariant', type: 'String', default: "'primary'", required: false, description: '确认按钮变体：primary, secondary, success, warning, danger' },
        { name: 'closeOnBackdrop', type: 'Boolean', default: 'true', required: false, description: '是否可以点击背景关闭弹窗' },
        { name: 'closeOnEsc', type: 'Boolean', default: 'true', required: false, description: '是否可以按ESC键关闭弹窗' },
      ],
      events: [
        { name: 'update:visible', params: 'visible: Boolean', description: '当弹窗显示状态改变时触发' },
        { name: 'close', params: '', description: '当弹窗关闭时触发' },
        { name: 'confirm', params: '', description: '当点击确认按钮时触发' },
      ],
      slots: [
        { name: 'default', scope: '', description: '弹窗主要内容，优先级高于content属性' },
        { name: 'title', scope: '', description: '自定义标题内容，优先级高于title属性' },
        { name: 'footer', scope: '{ close, confirm }', description: '自定义底部操作区域，提供close和confirm方法' },
      ]
    };
  } else if (component === 'Alert') {
    parameterModalData.value = {
      parameters: [
        { name: 'title', type: 'String', default: "''", required: false, description: '警告提示的标题' },
        { name: 'message', type: 'String', default: "''", required: false, description: '警告提示的消息内容' },
        { name: 'variant', type: 'String', default: "'default'", required: false, description: '警告类型：default, primary, secondary, success, warning, danger' },
        { name: 'visible', type: 'Boolean', default: 'true', required: false, description: '是否显示警告提示' },
        { name: 'closable', type: 'Boolean', default: 'false', required: false, description: '是否显示关闭按钮' },
        { name: 'icon', type: 'Component', default: 'null', required: false, description: '自定义图标组件，默认根据variant自动选择' },
        { name: 'showIcon', type: 'Boolean', default: 'true', required: false, description: '是否显示图标' },
        { name: 'iconSize', type: 'Number', default: '20', required: false, description: '图标大小' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '警告提示大小：sm, md, lg' },
        { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '是否为圆角样式' },
      ],
      events: [
        { name: 'close', params: '', description: '当点击关闭按钮时触发' },
      ],
      slots: [
        { name: 'default', scope: '', description: '自定义警告内容，优先级高于message属性' },
      ]
    };
  } else if (component === 'Dropdown') {
    parameterModalData.value = {
      parameters: [
        { name: 'triggerText', type: 'String', default: "'Open Menu'", required: false, description: '触发按钮显示的文字' },
        { name: 'items', type: 'Array', default: '', required: true, description: '下拉菜单项数组，支持label、value、icon、shortcut、divider、disabled、variant等属性' },
        { name: 'variant', type: 'String', default: "'default'", required: false, description: '触发按钮变体：default, primary, outline, ghost' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '触发按钮尺寸：sm, md, lg' },
        { name: 'disabled', type: 'Boolean', default: 'false', required: false, description: '是否禁用下拉菜单' },
        { name: 'rounded', type: 'Boolean', default: 'false', required: false, description: '圆角类型：false为微微圆角(rounded-lg)，true为椭圆形(rounded-3xl)' },
        { name: 'trigger', type: 'String', default: "'click'", required: false, description: '触发模式：click为点击触发，hover为悬停触发' },
        { name: 'prefixIcon', type: 'String', default: 'null', required: false, description: '触发按钮的前置图标SVG路径' },
        { name: 'placement', type: 'String', default: "'bottom-start'", required: false, description: '下拉菜单位置：bottom-start, bottom-end, top-start, top-end' },
        { name: 'closeOnClick', type: 'Boolean', default: 'true', required: false, description: '点击菜单项后是否自动关闭' },
        { name: 'autoClose', type: 'Boolean', default: 'true', required: false, description: '点击外部时是否自动关闭' },
        { name: 'hoverDelay', type: 'Number', default: '150', required: false, description: 'hover模式的延迟时间（毫秒），适用于悬停触发和离开的延迟' },
      ],
      events: [
        { name: 'select', params: 'item: Object', description: '当选择菜单项时触发，返回选中的项目对象' },
        { name: 'open', params: '', description: '当下拉菜单打开时触发' },
        { name: 'close', params: '', description: '当下拉菜单关闭时触发' },
      ],
      slots: []
    };
  } else if (component === 'Drawer') {
    parameterModalData.value = {
      parameters: [
        { name: 'visible', type: 'Boolean', default: 'false', required: false, description: '抽屉的显示状态，支持 v-model' },
        { name: 'title', type: 'String', default: "'Drawer Title'", required: false, description: '抽屉标题' },
        { name: 'content', type: 'String', default: "''", required: false, description: '抽屉内容文本' },
        { name: 'placement', type: 'String', default: "'right'", required: false, description: '抽屉出现位置：left, right, top, bottom' },
        { name: 'size', type: 'String', default: "'md'", required: false, description: '抽屉尺寸：sm, md, lg, xl, full' },
        { name: 'showHeader', type: 'Boolean', default: 'true', required: false, description: '是否显示头部区域' },
        { name: 'showFooter', type: 'Boolean', default: 'false', required: false, description: '是否显示底部操作区域' },
        { name: 'closable', type: 'Boolean', default: 'true', required: false, description: '是否显示关闭按钮' },
        { name: 'showCancelButton', type: 'Boolean', default: 'true', required: false, description: '是否显示取消按钮' },
        { name: 'showConfirmButton', type: 'Boolean', default: 'false', required: false, description: '是否显示确认按钮' },
        { name: 'cancelText', type: 'String', default: "'Close'", required: false, description: '取消按钮文本' },
        { name: 'confirmText', type: 'String', default: "'Confirm'", required: false, description: '确认按钮文本' },
        { name: 'confirmVariant', type: 'String', default: "'primary'", required: false, description: '确认按钮变体：primary, success, warning, danger' },
        { name: 'closeOnBackdrop', type: 'Boolean', default: 'true', required: false, description: '是否可以点击背景关闭抽屉' },
        { name: 'closeOnEsc', type: 'Boolean', default: 'true', required: false, description: '是否可以按ESC键关闭抽屉' },
      ],
      events: [
        { name: 'update:visible', params: 'visible: Boolean', description: '当抽屉显示状态改变时触发' },
        { name: 'close', params: '', description: '当抽屉关闭时触发' },
        { name: 'confirm', params: '', description: '当点击确认按钮时触发' },
      ],
      slots: [
        { name: 'default', scope: '', description: '抽屉主要内容，优先级高于content属性' },
        { name: 'title', scope: '', description: '自定义标题内容，优先级高于title属性' },
        { name: 'footer', scope: '{ close }', description: '自定义底部操作区域，提供close方法' },
      ]
    };
  }
  
  isParameterModalVisible.value = true;
};

const closeParameterModal = () => {
  isParameterModalVisible.value = false;
};

// Drawer事件处理函数
const openDrawer = (placement) => {
  currentDrawerPlacement.value = placement;
  currentDrawerSize.value = 'md';
  drawerStates.value.basic = true;
};

const openDrawerWithSize = (placement, size) => {
  currentDrawerPlacement.value = placement;
  currentDrawerSize.value = size;
  drawerStates.value.basic = true;
};

const openSettingsDrawer = () => {
  drawerStates.value.settings = true;
};

const openNotificationDrawer = () => {
  drawerStates.value.notification = true;
};

const openFormDrawer = () => {
  drawerStates.value.form = true;
};

const openDrawerModal = () => {
  modalTitle.value = 'Drawer 组件代码';
  modalCodeTabs.value = [
    {
      title: '使用方法',
      code: `<template>
  <!-- 基础抽屉 -->
  <drawer v-model:visible="drawerVisible" title="抽屉标题" placement="right">
    <p>这里是抽屉内容</p>
  </drawer>
  
  <!-- 设置不同方向 -->
  <drawer v-model:visible="leftDrawer" title="左侧抽屉" placement="left" />
  <drawer v-model:visible="topDrawer" title="顶部抽屉" placement="top" />
  <drawer v-model:visible="bottomDrawer" title="底部抽屉" placement="bottom" />
  
  <!-- 设置不同尺寸 -->
  <drawer v-model:visible="smallDrawer" title="小抽屉" size="sm" />
  <drawer v-model:visible="largeDrawer" title="大抽屉" size="lg" />
  
  <!-- 带footer的抽屉 -->
  <drawer 
    v-model:visible="formDrawer" 
    title="表单抽屉" 
    :show-footer="true"
    :show-confirm-button="true"
    confirm-text="保存"
    @confirm="handleSave"
  >
    <form>
      <input placeholder="请输入内容" />
    </form>
  </drawer>
  
  <!-- 自定义内容抽屉 -->
  <drawer v-model:visible="customDrawer" title="自定义抽屉">
    <template #title>
      <div class="flex items-center space-x-2">
        <settings-icon />
        <span>设置中心</span>
      </div>
    </template>
    
    <div class="space-y-4">
      <div>设置项 1</div>
      <div>设置项 2</div>
    </div>
    
    <template #footer="{ close }">
      <div class="flex justify-between">
        <button @click="resetSettings">重置</button>
        <div class="space-x-2">
          <button @click="close">取消</button>
          <button @click="saveSettings">保存</button>
        </div>
      </div>
    </template>
  </drawer>
</template>

<script setup>
import { ref } from 'vue';
import Drawer from './components/Drawer.vue';

const drawerVisible = ref(false);
const leftDrawer = ref(false);
const topDrawer = ref(false);
const bottomDrawer = ref(false);
const smallDrawer = ref(false);
const largeDrawer = ref(false);
const formDrawer = ref(false);
const customDrawer = ref(false);

const handleSave = () => {
  console.log('保存数据');
  formDrawer.value = false;
};

const resetSettings = () => {
  console.log('重置设置');
};

const saveSettings = () => {
  console.log('保存设置');
  customDrawer.value = false;
};
<\/script>`
    },
    {
      title: '组件源码',
      code: `<template>
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
        v-if="visible"
        class="fixed inset-0 z-50 flex"
        @click="handleBackdropClick"
      >
        <!-- 背景遮罩 -->
        <div class="absolute inset-0 bg-black/50 backdrop-blur-sm"></div>
        
        <!-- 抽屉内容 -->
        <Transition
          name="drawer-content"
          :enter-active-class="enterActiveClass"
          :enter-from-class="enterFromClass"
          :enter-to-class="enterToClass"
          :leave-active-class="leaveActiveClass"
          :leave-from-class="leaveFromClass"
          :leave-to-class="leaveToClass"
        >
          <div
            v-if="visible"
            :class="drawerClass"
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
                class="text-slate-400 hover:text-slate-600 transition-colors p-1 rounded-md hover:bg-slate-100"
              >
                <X :size="20" />
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
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { computed, watch, nextTick, onUnmounted } from 'vue';
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

// 抽屉主体样式
const drawerClass = computed(() => {
  const baseClasses = [
    'relative bg-white shadow-2xl overflow-hidden flex flex-col',
  ];

  // 位置和圆角
  switch (props.placement) {
    case 'left':
      baseClasses.push('h-full rounded-r-xl');
      break;
    case 'right':
      baseClasses.push('h-full rounded-l-xl ml-auto');
      break;
    case 'top':
      baseClasses.push('w-full rounded-b-xl');
      break;
    case 'bottom':
      baseClasses.push('w-full rounded-t-xl mt-auto');
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

// 省略更多代码...
<\/script>`
    }
  ];
  isModalVisible.value = true;
};
</script>

<style>
/* 瀑布流布局样式 - 手机端自适应 */
.masonry-container {
  columns: 1;
  column-gap: 1.5rem;
  padding: 0;
}

@media (min-width: 768px) {
  .masonry-container {
    columns: 2;
    column-gap: 2rem;
  }
}

.masonry-item {
  display: inline-block;
  width: 100%;
  margin-bottom: 2rem;
  break-inside: avoid;
  page-break-inside: avoid;
}

/* 确保卡片不会被截断 */
.masonry-item * {
  break-inside: avoid;
}

/* 优化加载动画 */
.masonry-item:hover {
  transform: translateY(-2px);
  transition: transform 0.2s ease-in-out;
}
</style>
