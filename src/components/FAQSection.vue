<script setup lang="ts">
import { ref } from 'vue'

const openIndex = ref<number | null>(0)

const faqs = [
  {
    q: '父母下单的方式是什么？',
    a: '父母只需拨打专属电话或通过微信语音下单，说出需求即可。不需要操作手机 App，一个电话就能完成下单。子女端会收到订单通知，确认后接单跑腿。',
  },
  {
    q: '服务范围覆盖哪些区域？',
    a: '目前为私人专属服务，覆盖指定社区。下单时会确认地址是否在服务范围内。如果您所在的区域暂时不在覆盖范围，可以留下联系方式，后续扩展会优先通知您。',
  },
  {
    q: '每个产品的 Basic / Standard / Pro 有什么区别？',
    a: 'Basic 适合轻度需求，每月次数较少、功能基础；Standard 是最受欢迎的档位，功能全面、次数适中，性价比最优；Pro 适合高频需求，次数最多，还包含专属对接、指定时间段等增值权益。您可以随时升降级。',
  },
  {
    q: '首月半价是怎么算的？',
    a: '首月为新用户体验价，约为原价 5 折。例如 Curio 代买 Standard 原价 44.9/月，首月仅 22.9 元；Curio 陪护 Basic 原价 44.9/月，首月 22.9 元。CurioOne 原价 249.9/月，首月 124.9 元。次月起恢复原价。',
  },
  {
    q: '订阅后可以随时取消吗？',
    a: '当然可以。所有订阅方案均为连续包月，不设合约期。您可以在任何时候取消订阅，取消后当月已支付的费用不会退还，但服务持续到本计费周期结束。',
  },
  {
    q: '单次付费和订阅有什么区别？',
    a: '单次付费即用即付：代买 3.5 元/次、代取 2.5 元/次、家政 7 元/次、网管 9 元/次、陪护 12 元/次、代办 5 元/次。订阅制每月有固定次数额度，折算下来更划算，且 Standard 及以上享有优先接单权益。经常需要服务的建议订阅，偶尔使用的可以单次付费。',
  },
  {
    q: 'CurioOne 和单独订阅有什么区别？',
    a: 'CurioOne 是捆绑包，包含全部六大产品（代买、代取、家政、网管、陪护、代办），不限服务次数，且享有优先派单、专属跑腿员、每月健康关怀报告等权益。单独订阅每个产品只能使用对应服务，且有次数限制。CurioOne 249.9/月，约为全部 Pro 档总价（372.4/月）的 67%，每月省 122.5 元。',
  },
]
</script>

<template>
  <section id="faq" class="py-24 lg:py-32 bg-cream-dark/50 relative">
    <div class="max-w-3xl mx-auto px-6 lg:px-8">
      <div class="mb-16">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">05</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">FAQ</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">
          常见问题
        </h2>
        <p class="text-lg text-ink-soft leading-relaxed">
          还有疑问？随时联系我们。
        </p>
      </div>

      <div class="space-y-3">
        <div
          v-for="(faq, i) in faqs"
          :key="i"
          class="bg-white rounded-xl border border-border-warm overflow-hidden transition-all duration-300"
          :class="openIndex === i ? 'shadow-md' : ''"
        >
          <button
            class="w-full flex items-center justify-between px-6 py-5 text-left"
            @click="openIndex = openIndex === i ? null : i"
          >
            <span class="font-medium text-ink pr-4">{{ faq.q }}</span>
            <svg
              class="w-5 h-5 text-muted flex-shrink-0 transition-transform duration-300"
              :class="openIndex === i ? 'rotate-180' : ''"
              fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7" />
            </svg>
          </button>
          <transition
            enter-active-class="transition-all duration-300 ease-out"
            enter-from-class="max-h-0 opacity-0"
            enter-to-class="max-h-96 opacity-100"
            leave-active-class="transition-all duration-200 ease-in"
            leave-from-class="max-h-96 opacity-100"
            leave-to-class="max-h-0 opacity-0"
          >
            <div v-if="openIndex === i" class="overflow-hidden">
              <p class="px-6 pb-5 text-sm text-ink-soft leading-relaxed">{{ faq.a }}</p>
            </div>
          </transition>
        </div>
      </div>

      <div class="mt-12 text-center">
        <p class="text-sm text-muted mb-3">还有其他问题？</p>
        <a href="#cta" class="inline-flex items-center gap-2 text-coral hover:underline">
          联系我们
          <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
        </a>
      </div>
    </div>
  </section>
</template>
