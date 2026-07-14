<script setup lang="ts">
const values = [
  {
    title: '一个人，一份心',
    desc: '不是平台，不是中介。每一次服务都由我亲自完成，确保质量。',
    icon: 'user',
  },
  {
    title: '把家长当家人',
    desc: '服务过程中多问一句、多帮一步，因为那是别人的父母。',
    icon: 'heart',
  },
  {
    title: '全程透明',
    desc: '每一步都拍照反馈，子女随时查看，放心托付。',
    icon: 'eye',
  },
]
</script>

<template>
  <section id="about" class="py-24 lg:py-32 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <div class="grid lg:grid-cols-2 gap-12 lg:gap-16 items-center">
        <!-- Left: Visual -->
        <div class="relative">
          <div class="aspect-square max-w-md mx-auto relative">
            <!-- Background shapes -->
            <div class="absolute inset-0 bg-gradient-to-br from-coral-light to-amber-light rounded-3xl rotate-3"></div>
            <div class="absolute inset-0 bg-white rounded-3xl border border-border-warm flex items-center justify-center -rotate-1">
              <div class="text-center p-12">
                <div class="w-24 h-24 rounded-full bg-gradient-to-br from-coral to-coral-dark mx-auto mb-6 flex items-center justify-center">
                  <svg class="w-12 h-12 text-cream" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                  </svg>
                </div>
                <p class="font-semibold text-ink text-lg mb-1">跑腿员 · 小陈</p>
                <p class="text-sm text-muted">3 年跑腿服务经验</p>
                <div class="mt-6 pt-6 border-t border-border-warm">
                  <div class="flex justify-center gap-6 text-center">
                    <div>
                      <p class="text-2xl font-bold text-ink">3年</p>
                      <p class="text-xs text-muted">服务经验</p>
                    </div>
                    <div>
                      <p class="text-2xl font-bold text-ink">500+</p>
                      <p class="text-xs text-muted">服务家庭</p>
                    </div>
                    <div>
                      <p class="text-2xl font-bold text-ink">100%</p>
                      <p class="text-xs text-muted">好评率</p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Content -->
        <div>
          <div class="flex items-center gap-3 mb-4">
            <span class="font-mono text-xs text-muted">05</span>
            <div class="w-8 h-px bg-border-warm"></div>
            <span class="text-xs text-muted uppercase tracking-wider">关于</span>
          </div>
          <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-6">
            一个人，<br />一份心
          </h2>
          <p class="text-lg text-ink-soft leading-relaxed mb-4">
            我叫小陈，做跑腿三年了。最开始是帮自己爸妈买菜、跑医院，后来发现身边很多朋友也有同样的困扰——在外地工作，挂念家里的父母，却没法亲自照顾。
          </p>
          <p class="text-base text-ink-soft leading-relaxed mb-8">
            于是我开始了 Curio，一个人、一份心，专门为家长跑腿。不是平台派单，不是中介抽成，每一次服务都由我亲自完成。我把每一位家长都当作自己的父母来照顾。
          </p>

          <!-- Values -->
          <div class="space-y-5">
            <div v-for="value in values" :key="value.title" class="flex gap-4">
              <div class="w-10 h-10 rounded-lg bg-cream-dark flex items-center justify-center flex-shrink-0">
                <svg v-if="value.icon === 'user'" class="w-5 h-5 text-coral" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" /></svg>
                <svg v-else-if="value.icon === 'heart'" class="w-5 h-5 text-coral" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
                <svg v-else class="w-5 h-5 text-coral" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /><path stroke-linecap="round" stroke-linejoin="round" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" /></svg>
              </div>
              <div>
                <h3 class="font-semibold text-ink mb-1">{{ value.title }}</h3>
                <p class="text-sm text-ink-soft leading-relaxed">{{ value.desc }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
