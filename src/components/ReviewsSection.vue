<script setup lang="ts">
const reviews = [
  {
    name: '李女士',
    role: '女儿 · 远在北京',
    avatar: '李',
    color: 'coral',
    content: '我在北京工作，爸妈在老家。以前总担心他们买菜不方便、看病没人陪。用了 Curio 之后，我直接在手机上下单，跑腿员上门帮我爸妈买菜、陪他们去医院。爸妈说服务的人特别耐心，我也安心多了。',
    rating: 5,
  },
  {
    name: '张先生',
    role: '儿子 · 远在上海',
    avatar: '张',
    color: 'teal',
    content: '订了旗舰版，每周固定两次家政服务，帮妈妈打扫卫生、整理房间。妈妈一开始还不好意思，后来每次都盼着跑腿员来。月度健康报告也很用心，能看到爸妈的生活状况。',
    rating: 5,
  },
  {
    name: '王女士',
    role: '女儿 · 远在深圳',
    avatar: '王',
    color: 'amber',
    content: '爸爸需要定期去银行办手续，他腿脚不方便。通过 Curio 约了陪护代办，跑腿员全程陪同，办完还拍照发给我确认。2 块钱一次的单次服务真的太良心了，后来直接包了月。',
    rating: 5,
  },
]
</script>

<template>
  <section id="reviews" class="py-24 lg:py-32 bg-cream-dark/50 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <!-- Section header -->
      <div class="max-w-2xl mb-16">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">04</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">评价</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">
          家长满意，<br />子女安心
        </h2>
        <p class="text-lg text-ink-soft leading-relaxed">
          来听听那些远在他乡的子女们怎么说。
        </p>
      </div>

      <!-- Reviews grid -->
      <div class="grid md:grid-cols-3 gap-6">
        <div
          v-for="review in reviews"
          :key="review.name"
          class="bg-white rounded-2xl border border-border-warm p-8 hover:shadow-lg hover:shadow-ink/5 transition-shadow duration-300"
        >
          <!-- Stars -->
          <div class="flex gap-0.5 mb-4">
            <svg v-for="i in review.rating" :key="i" class="w-4 h-4 text-amber" fill="currentColor" viewBox="0 0 20 20">
              <path d="M10 15l-5.878 3.09 1.123-6.545L.49 6.91l6.572-.955L10 0l2.938 5.955 6.572.955-4.755 4.635 1.123 6.545z" />
            </svg>
          </div>

          <!-- Content -->
          <p class="text-sm text-ink-soft leading-relaxed mb-6">{{ review.content }}</p>

          <!-- Author -->
          <div class="flex items-center gap-3 pt-4 border-t border-border-warm">
            <div
              class="w-10 h-10 rounded-full flex items-center justify-center font-medium text-sm"
              :class="{
                'bg-coral-light text-coral': review.color === 'coral',
                'bg-teal-light text-teal': review.color === 'teal',
                'bg-amber-light text-amber': review.color === 'amber',
              }"
            >
              {{ review.avatar }}
            </div>
            <div>
              <p class="text-sm font-medium text-ink">{{ review.name }}</p>
              <p class="text-xs text-muted">{{ review.role }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- Stats bar -->
      <div class="mt-16 grid grid-cols-2 md:grid-cols-4 gap-8 pt-12 border-t border-border-warm">
        <div class="text-center">
          <p class="text-3xl font-bold text-ink mb-1">500+</p>
          <p class="text-sm text-muted">服务家庭</p>
        </div>
        <div class="text-center">
          <p class="text-3xl font-bold text-ink mb-1">12,000+</p>
          <p class="text-sm text-muted">完成订单</p>
        </div>
        <div class="text-center">
          <p class="text-3xl font-bold text-ink mb-1">100%</p>
          <p class="text-sm text-muted">好评率</p>
        </div>
        <div class="text-center">
          <p class="text-3xl font-bold text-ink mb-1">30min</p>
          <p class="text-sm text-muted">平均响应</p>
        </div>
      </div>
    </div>
  </section>
</template>
