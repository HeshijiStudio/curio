<script setup lang="ts">
const year = new Date().getFullYear()

const links = {
  服务: ['代买代取', '家政服务', '陪护代办', 'All-in-One 全家桶'],
  公司: ['关于我们', '服务流程', '用户评价', '加入我们'],
  支持: ['常见问题', '联系客服', '服务条款', '隐私政策'],
}
</script>

<template>
  <footer class="border-t border-border-warm py-16 bg-cream">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-12">
        <!-- Brand -->
        <div class="col-span-2 md:col-span-1">
          <div class="flex items-center gap-2 mb-4">
            <div class="w-8 h-8 rounded-lg bg-ink flex items-center justify-center">
              <span class="text-cream font-bold text-lg leading-none">C</span>
            </div>
            <span class="font-semibold text-lg tracking-tight text-ink">Curio</span>
          </div>
          <p class="text-sm text-muted leading-relaxed max-w-xs">
            你尽孝，我来跑。专为家长设计的跑腿服务。
          </p>
        </div>

        <!-- Link columns -->
        <div v-for="(items, category) in links" :key="category">
          <h4 class="text-sm font-semibold text-ink mb-4">{{ category }}</h4>
          <ul class="space-y-2.5">
            <li v-for="item in items" :key="item">
              <a href="#" class="text-sm text-muted hover:text-coral transition-colors">{{ item }}</a>
            </li>
          </ul>
        </div>
      </div>

      <!-- Bottom bar -->
      <div class="pt-8 border-t border-border-warm flex flex-col sm:flex-row items-center justify-between gap-4">
        <p class="text-sm text-muted">© {{ year }} Curio. 保留所有权利.</p>
        <div class="flex items-center gap-6">
          <a href="#" class="text-sm text-muted hover:text-coral transition-colors">微信</a>
          <a href="#" class="text-sm text-muted hover:text-coral transition-colors">小红书</a>
          <a href="#" class="text-sm text-muted hover:text-coral transition-colors">抖音</a>
        </div>
      </div>
    </div>
  </footer>
</template>
