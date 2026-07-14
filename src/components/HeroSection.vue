<script setup lang="ts">
</script>

<template>
  <section class="relative pt-32 pb-20 lg:pt-40 lg:pb-28 overflow-hidden">
    <!-- Background gradient -->
    <div class="absolute inset-0 -z-10">
      <div class="absolute top-0 left-1/2 -translate-x-1/2 w-[800px] h-[600px] bg-gradient-to-b from-coral-light/40 via-amber-light/20 to-transparent rounded-full blur-3xl"></div>
      <div class="absolute top-40 right-0 w-[400px] h-[400px] bg-teal-light/30 rounded-full blur-3xl"></div>
    </div>

    <div class="max-w-4xl mx-auto px-6 lg:px-8 text-center">
      <!-- Badge -->
      <div class="inline-flex items-center gap-2 px-4 py-1.5 mb-8 bg-white/60 backdrop-blur-sm border border-border-warm rounded-full animate-fade-in">
        <span class="w-2 h-2 rounded-full bg-coral animate-pulse-soft"></span>
        <span class="text-sm text-ink-soft">家长下单，子女接单</span>
      </div>

      <!-- Headline -->
      <h1 class="text-5xl md:text-6xl lg:text-7xl font-bold tracking-tight text-ink leading-[1.05] mb-6 animate-fade-up">
        父母需要，
        <br />
        <span class="relative inline-block">
          <span class="relative z-10">我来跑。</span>
          <svg class="absolute -bottom-2 left-0 w-full z-0" viewBox="0 0 300 12" fill="none" preserveAspectRatio="none">
            <path d="M2 8C50 3 150 3 298 8" stroke="#D97757" stroke-width="4" stroke-linecap="round" />
          </svg>
        </span>
      </h1>

      <!-- Subheadline -->
      <p class="text-lg md:text-xl text-ink-soft leading-relaxed max-w-2xl mx-auto mb-10 animate-fade-up" style="animation-delay: 0.15s">
        父母一个电话下单，子女接单跑腿。<br class="hidden sm:block" />
        代买代取、家政网管、陪护代办——让照顾父母更简单。
      </p>

      <!-- CTAs -->
      <div class="flex flex-col sm:flex-row items-center justify-center gap-4 mb-16 animate-fade-up" style="animation-delay: 0.3s">
        <a
          href="#pricing"
          class="w-full sm:w-auto px-8 py-3.5 bg-ink text-cream font-medium rounded-full hover:bg-coral transition-all duration-300 hover:shadow-xl hover:shadow-coral/20 hover:-translate-y-0.5"
        >
          立即开始 — 首月半价
        </a>
        <a
          href="#services"
          class="w-full sm:w-auto px-8 py-3.5 bg-white/60 backdrop-blur-sm border border-border-warm text-ink font-medium rounded-full hover:bg-white hover:border-coral/30 transition-all duration-300"
        >
          了解服务
        </a>
      </div>

      <!-- Trust indicators -->
      <div class="flex flex-wrap items-center justify-center gap-x-8 gap-y-3 animate-fade-in" style="animation-delay: 0.5s">
        <div class="flex items-center gap-2">
          <svg class="w-4 h-4 text-coral" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
          <span class="text-sm text-ink-soft">私人专属服务</span>
        </div>
        <div class="flex items-center gap-2">
          <svg class="w-4 h-4 text-coral" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
          <span class="text-sm text-ink-soft">30分钟响应</span>
        </div>
        <div class="flex items-center gap-2">
          <svg class="w-4 h-4 text-coral" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"/></svg>
          <span class="text-sm text-ink-soft">上门服务</span>
        </div>
      </div>
    </div>

    <!-- Floating order card -->
    <div class="max-w-2xl mx-auto px-6 lg:px-8 mt-16 animate-fade-up" style="animation-delay: 0.6s">
      <div class="relative bg-white rounded-2xl shadow-xl shadow-ink/5 border border-border-warm overflow-hidden">
        <!-- Card header -->
        <div class="flex items-center justify-between px-6 py-4 border-b border-border-warm">
          <div class="flex items-center gap-2">
            <div class="w-2.5 h-2.5 rounded-full bg-coral/30"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-amber/30"></div>
            <div class="w-2.5 h-2.5 rounded-full bg-teal/30"></div>
          </div>
          <span class="text-xs text-muted font-mono">订单 #20260714</span>
        </div>
        <!-- Card body -->
        <div class="p-6 text-left">
          <div class="flex items-start justify-between mb-4">
            <div>
              <p class="text-xs text-muted mb-1">父母下单</p>
              <p class="text-sm font-medium text-ink">帮我去菜市场买点菜</p>
            </div>
            <span class="px-2.5 py-1 bg-teal-light text-teal text-xs font-medium rounded-full">子女已接单</span>
          </div>
          <div class="space-y-2.5">
            <div class="flex items-center gap-3 text-sm">
              <div class="w-7 h-7 rounded-full bg-coral-light flex items-center justify-center flex-shrink-0">
                <svg class="w-3.5 h-3.5 text-coral" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg>
              </div>
              <span class="text-ink-soft">菜市场代买 · 西红柿、鸡蛋、青菜</span>
            </div>
            <div class="flex items-center gap-3 text-sm">
              <div class="w-7 h-7 rounded-full bg-teal-light flex items-center justify-center flex-shrink-0">
                <svg class="w-3.5 h-3.5 text-teal" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
              </div>
              <span class="text-ink-soft">配送至 · 朝阳区幸福小区 3-2-501</span>
            </div>
            <div class="flex items-center gap-3 text-sm">
              <div class="w-7 h-7 rounded-full bg-amber-light flex items-center justify-center flex-shrink-0">
                <svg class="w-3.5 h-3.5 text-amber" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/></svg>
              </div>
              <span class="text-ink-soft">预计 30 分钟内送达</span>
            </div>
          </div>
          <div class="mt-5 pt-4 border-t border-border-warm flex items-center justify-between">
            <span class="text-xs text-muted">Curio 代买 Standard · 20次/月</span>
            <span class="text-sm font-semibold text-ink">¥2.00 / 次</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
