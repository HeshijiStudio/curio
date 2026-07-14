<script setup lang="ts">
import { ref } from 'vue'

const billing = ref<'subscription' | 'single'>('subscription')
const activeProduct = ref(0)

// 定价策略：
// Basic = 钩子价，极低门槛吸引用户进入
// Standard = 利润主力，性价比最优，推荐档位
// Pro = 升级档，与 Standard 差价小，诱导升级
// 首月 ≈ 5折，极具诱惑力
const products = [
  {
    name: '代买',
    fullName: 'Curio 代买',
    subtitle: '菜场超市 · 代买代购',
    icon: 'shopping',
    color: 'coral',
    single: 3.5,
    tiers: [
      { name: 'Basic', monthly: 22.9, firstMonth: 11.9, count: '8 次/月', perUse: '2.86', features: ['菜市场代买', '超市代购', '30分钟响应'] },
      { name: 'Standard', monthly: 44.9, firstMonth: 22.9, count: '20 次/月', perUse: '2.25', popular: true, features: ['Basic 全部权益', '日用品采购', '药品代买', '优先接单'] },
      { name: 'Pro', monthly: 54.9, firstMonth: 27.9, count: '35 次/月', perUse: '1.57', features: ['Standard 全部权益', '不限品类', '指定时间段', '专属对接'] },
    ],
  },
  {
    name: '代取',
    fullName: 'Curio 代取',
    subtitle: '快递物品 · 代取代送',
    icon: 'package',
    color: 'amber',
    single: 2.5,
    tiers: [
      { name: 'Basic', monthly: 18.9, firstMonth: 9.9, count: '12 次/月', perUse: '1.58', features: ['快递代取', '物品代送', '30分钟响应'] },
      { name: 'Standard', monthly: 33.9, firstMonth: 16.9, count: '25 次/月', perUse: '1.36', popular: true, features: ['Basic 全部权益', '代寄快递', '大件搬运', '优先接单'] },
      { name: 'Pro', monthly: 43.9, firstMonth: 21.9, count: '40 次/月', perUse: '1.10', features: ['Standard 全部权益', '不限重量', '指定时间段', '专属对接'] },
    ],
  },
  {
    name: '家政',
    fullName: 'Curio 家政',
    subtitle: '清洁收纳 · 居家打理',
    icon: 'broom',
    color: 'teal',
    single: 7,
    tiers: [
      { name: 'Basic', monthly: 34.9, firstMonth: 17.9, count: '4 次/月', perUse: '8.73', features: ['基础清洁', '地面打扫', '垃圾清理'] },
      { name: 'Standard', monthly: 54.9, firstMonth: 27.9, count: '8 次/月', perUse: '6.86', popular: true, features: ['Basic 全部权益', '收纳整理', '衣物洗晒', '玻璃擦拭'] },
      { name: 'Pro', monthly: 74.9, firstMonth: 37.9, count: '12 次/月', perUse: '6.24', features: ['Standard 全部权益', '深度清洁', '厨房油烟处理', '专属对接'] },
    ],
  },
  {
    name: '网管',
    fullName: 'Curio 网管',
    subtitle: '网络检测 · 电脑手机维修',
    icon: 'wrench',
    color: 'teal',
    single: 9,
    tiers: [
      { name: 'Basic', monthly: 28.9, firstMonth: 14.9, count: '3 次/月', perUse: '9.63', features: ['网络测速排障', 'WiFi优化', '手机清理加速'] },
      { name: 'Standard', monthly: 49.9, firstMonth: 24.9, count: '6 次/月', perUse: '8.32', popular: true, features: ['Basic 全部权益', '电脑维修调试', '系统重装', '软件安装'] },
      { name: 'Pro', monthly: 64.9, firstMonth: 32.9, count: '10 次/月', perUse: '6.49', features: ['Standard 全部权益', '路由器配置', '智能家居设置', '远程技术支持'] },
    ],
  },
  {
    name: '陪护',
    fullName: 'Curio 陪护',
    subtitle: '陪同就医 · 健康陪护',
    icon: 'heart',
    color: 'coral',
    single: 12,
    tiers: [
      { name: 'Basic', monthly: 44.9, firstMonth: 22.9, count: '3 次/月 (每次2h)', perUse: '14.97', features: ['陪同就医', '取药送药', '就诊排队'] },
      { name: 'Standard', monthly: 64.9, firstMonth: 32.9, count: '5 次/月 (每次3h)', perUse: '12.98', popular: true, features: ['Basic 全部权益', '健康陪护', '康复陪伴', '就诊记录反馈'] },
      { name: 'Pro', monthly: 84.9, firstMonth: 42.9, count: '8 次/月 (每次4h)', perUse: '10.61', features: ['Standard 全部权益', '半日陪护', '健康报告', '专属对接'] },
    ],
  },
  {
    name: '代办',
    fullName: 'Curio 代办',
    subtitle: '代办手续 · 代缴费',
    icon: 'document',
    color: 'amber',
    single: 5,
    tiers: [
      { name: 'Basic', monthly: 22.9, firstMonth: 11.9, count: '8 次/月', perUse: '2.86', features: ['代缴费', '简单跑腿', '30分钟响应'] },
      { name: 'Standard', monthly: 37.9, firstMonth: 18.9, count: '15 次/月', perUse: '2.53', popular: true, features: ['Basic 全部权益', '代办手续', '银行办事', '优先接单'] },
      { name: 'Pro', monthly: 49.9, firstMonth: 24.9, count: '25 次/月', perUse: '2.00', features: ['Standard 全部权益', '证件代办', '加急办理', '专属对接'] },
    ],
  },
]

// CurioOne: 249.9/月，首月 124.9（半价）
// individualSum = 全部 Pro 档之和: 54.9+43.9+74.9+64.9+84.9+49.9 = 372.4
const bundle = {
  name: 'CurioOne',
  tagline: '一次订阅，全部六大产品不限次',
  monthly: 249.9,
  firstMonth: 124.9,
  individualSum: 372.4, // Pro tiers: 54.9+43.9+74.9+64.9+84.9+49.9
  features: [
    '六大产品全部包含',
    '不限服务次数',
    '优先派单 + 专属跑腿员',
    '每月健康关怀报告',
    '紧急情况 24h 响应',
    '节假日无加价',
    '家属实时查看服务记录',
    '免费取消，随时续费',
  ],
}

const current = ref(products[0])

function selectProduct(i: number) {
  activeProduct.value = i
  current.value = products[i]
}
</script>

<template>
  <section id="pricing" class="py-24 lg:py-32 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <!-- Section header -->
      <div class="max-w-2xl mb-12">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">03</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">定价</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">
          六大产品，<br />三档选择
        </h2>
        <p class="text-lg text-ink-soft leading-relaxed">
          每个产品均有 Basic / Standard / Pro 三档。首月半价，连续包月随时取消。
        </p>
      </div>

      <!-- Billing toggle -->
      <div class="flex items-center justify-center gap-1 p-1 bg-cream-dark rounded-full w-fit mx-auto mb-8">
        <button
          class="px-6 py-2 text-sm font-medium rounded-full transition-all duration-300"
          :class="billing === 'subscription' ? 'bg-ink text-cream shadow-md' : 'text-ink-soft hover:text-ink'"
          @click="billing = 'subscription'"
        >
          订阅制
        </button>
        <button
          class="px-6 py-2 text-sm font-medium rounded-full transition-all duration-300"
          :class="billing === 'single' ? 'bg-ink text-cream shadow-md' : 'text-ink-soft hover:text-ink'"
          @click="billing = 'single'"
        >
          单次付费
        </button>
      </div>

      <!-- ===== Subscription mode ===== -->
      <div v-if="billing === 'subscription'">
        <!-- Product tabs -->
        <div class="flex flex-wrap items-center justify-center gap-2 mb-10">
          <button
            v-for="(p, i) in products"
            :key="p.name"
            class="px-4 py-2 text-sm font-medium rounded-full border transition-all duration-300"
            :class="activeProduct === i
              ? 'bg-ink text-cream border-ink'
              : 'bg-white text-ink-soft border-border-warm hover:border-coral/40'"
            @click="selectProduct(i)"
          >
            {{ p.fullName }}
          </button>
        </div>

        <!-- 3-tier cards for current product -->
        <transition mode="out-in"
          enter-active-class="transition-all duration-300 ease-out"
          enter-from-class="opacity-0 translate-y-2"
          leave-active-class="transition-all duration-150 ease-in"
          leave-to-class="opacity-0 -translate-y-2"
        >
          <div :key="activeProduct" class="grid md:grid-cols-3 gap-6 mb-12">
            <div
              v-for="tier in current.tiers"
              :key="tier.name"
              class="relative bg-white rounded-2xl border p-8 transition-all duration-300 hover:shadow-xl hover:shadow-ink/5"
              :class="tier.popular ? 'border-coral/40 shadow-lg ring-1 ring-coral/10 md:scale-105' : 'border-border-warm'"
            >
              <!-- Popular badge -->
              <div v-if="tier.popular" class="absolute -top-3 left-1/2 -translate-x-1/2">
                <span class="px-4 py-1 bg-coral text-cream text-xs font-medium rounded-full">最受欢迎</span>
              </div>

              <!-- Tier name -->
              <div class="mb-5">
                <h3 class="text-lg font-semibold text-ink mb-1">{{ current.fullName }} · {{ tier.name }}</h3>
                <p class="text-sm text-muted">{{ current.subtitle }}</p>
              </div>

              <!-- Price -->
              <div class="mb-1">
                <div class="flex items-baseline gap-1">
                  <span class="text-4xl font-bold text-ink">¥{{ tier.firstMonth }}</span>
                  <span class="text-sm text-muted">/ 首月</span>
                </div>
                <div class="flex items-center gap-2 mt-1">
                  <p class="text-xs text-coral">次月 ¥{{ tier.monthly }}/月</p>
                  <span class="text-muted">·</span>
                  <p class="text-xs text-muted">{{ tier.count }}</p>
                </div>
                <p class="text-xs text-teal mt-1.5 font-medium">约 ¥{{ tier.perUse }}/次</p>
              </div>

              <div class="my-6 h-px bg-border-warm"></div>

              <!-- Features -->
              <ul class="space-y-3 mb-8">
                <li v-for="feature in tier.features" :key="feature" class="flex items-center gap-2.5 text-sm text-ink-soft">
                  <svg
                    class="w-4 h-4 flex-shrink-0"
                    :class="{ 'text-coral': current.color === 'coral', 'text-teal': current.color === 'teal', 'text-amber': current.color === 'amber' }"
                    fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"
                  ><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
                  {{ feature }}
                </li>
              </ul>

              <!-- CTA -->
              <a
                href="#cta"
                class="block w-full py-3 text-center font-medium rounded-full transition-all duration-300"
                :class="tier.popular ? 'bg-ink text-cream hover:bg-coral' : 'bg-cream-dark text-ink hover:bg-border-warm'"
              >
                选择 {{ tier.name }}
              </a>
            </div>
          </div>
        </transition>

        <!-- Single charge info for current product -->
        <div class="max-w-2xl mx-auto bg-cream-dark/60 rounded-2xl p-6 mb-12 flex items-center justify-between">
          <div>
            <p class="text-sm text-muted mb-1">不想订阅？</p>
            <p class="text-sm text-ink-soft">{{ current.fullName }} 也支持单次付费</p>
          </div>
          <div class="text-right">
            <span class="text-2xl font-bold text-ink">¥{{ current.single }}</span>
            <span class="text-sm text-muted">/ 次</span>
            <button class="ml-4 text-sm text-coral hover:underline" @click="billing = 'single'">查看单次 →</button>
          </div>
        </div>

        <!-- CurioOne Bundle -->
        <div class="relative bg-gradient-to-br from-ink to-ink-soft rounded-3xl p-8 lg:p-12 overflow-hidden">
          <div class="absolute top-0 right-0 w-96 h-96 bg-coral/10 rounded-full blur-3xl -translate-y-1/2 translate-x-1/4"></div>
          <div class="absolute bottom-0 left-0 w-64 h-64 bg-teal/10 rounded-full blur-3xl translate-y-1/2"></div>

          <div class="relative grid lg:grid-cols-2 gap-8 lg:gap-12 items-center">
            <div>
              <div class="inline-flex items-center gap-2 px-3 py-1 bg-coral/20 border border-coral/30 rounded-full mb-6">
                <svg class="w-3.5 h-3.5 text-coral-light" fill="currentColor" viewBox="0 0 20 20"><path d="M10 15l-5.878 3.09 1.123-6.545L.49 6.91l6.572-.955L10 0l2.938 5.955 6.572.955-4.755 4.635 1.123 6.545z"/></svg>
                <span class="text-xs text-coral-light font-medium">最超值 · 省钱之选</span>
              </div>
              <h3 class="text-2xl lg:text-3xl font-bold text-cream mb-3">{{ bundle.name }}</h3>
              <p class="text-cream/60 text-base mb-8">{{ bundle.tagline }}</p>
              <div class="flex items-baseline gap-2 mb-2">
                <span class="text-5xl font-bold text-cream">¥{{ bundle.firstMonth }}</span>
                <span class="text-cream/50 text-sm">/ 首月</span>
              </div>
              <p class="text-coral-light text-sm">次月 ¥{{ bundle.monthly }}/月 · 连续包月</p>
              <div class="mt-4 inline-flex items-center gap-2 px-3 py-1.5 bg-teal/20 border border-teal/30 rounded-lg">
                <svg class="w-4 h-4 text-teal-light" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg>
                <span class="text-sm text-teal-light font-medium">较单独订阅全部 Pro 省 ¥{{ (bundle.individualSum - bundle.monthly).toFixed(1) }} / 月</span>
              </div>
            </div>
            <div>
              <ul class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-8">
                <li v-for="feature in bundle.features" :key="feature" class="flex items-start gap-2.5 text-sm text-cream/80">
                  <svg class="w-4 h-4 text-coral-light flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
                  {{ feature }}
                </li>
              </ul>
              <a href="#cta" class="inline-flex items-center gap-2 px-8 py-3.5 bg-coral text-cream font-medium rounded-full hover:bg-coral-dark transition-all duration-300 hover:shadow-xl hover:shadow-coral/30">
                选择 CurioOne
                <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg>
              </a>
            </div>
          </div>
        </div>
      </div>

      <!-- ===== Single charge mode ===== -->
      <div v-else class="max-w-4xl mx-auto">
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
          <div
            v-for="p in products"
            :key="p.name"
            class="bg-white rounded-2xl border border-border-warm p-6 text-center hover:shadow-lg hover:shadow-ink/5 transition-all duration-300"
          >
            <div
              class="w-12 h-12 rounded-xl flex items-center justify-center mx-auto mb-4"
              :class="{ 'bg-coral-light': p.color === 'coral', 'bg-teal-light': p.color === 'teal', 'bg-amber-light': p.color === 'amber' }"
            >
              <svg v-if="p.icon === 'shopping'" class="w-6 h-6" :class="{ 'text-coral': p.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
              <svg v-else-if="p.icon === 'package'" class="w-6 h-6" :class="{ 'text-amber': p.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
              <svg v-else-if="p.icon === 'broom'" class="w-6 h-6" :class="{ 'text-teal': p.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.324.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 011.37.49l1.296 2.247a1.125 1.125 0 01-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 010 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 01-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 01-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 01-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 01-1.369-.49l-1.297-2.247a1.125 1.125 0 01.26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 010-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 01-.26-1.43l1.297-2.247a1.125 1.125 0 011.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28z" /><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
              <svg v-else-if="p.icon === 'wrench'" class="w-6 h-6" :class="{ 'text-teal': p.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
              <svg v-else-if="p.icon === 'heart'" class="w-6 h-6" :class="{ 'text-coral': p.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
              <svg v-else class="w-6 h-6" :class="{ 'text-amber': p.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 002.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 00-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25z" /></svg>
            </div>
            <h3 class="text-sm font-semibold text-ink mb-1">{{ p.fullName }}</h3>
            <p class="text-xs text-muted mb-3">{{ p.subtitle }}</p>
            <div class="flex items-baseline justify-center gap-0.5">
              <span class="text-3xl font-bold text-ink">¥{{ p.single }}</span>
              <span class="text-xs text-muted">/次</span>
            </div>
          </div>
        </div>
        <p class="text-center text-sm text-muted mt-8">
          经常需要服务？
          <button class="text-coral hover:underline" @click="billing = 'subscription'">看看订阅方案 →</button>
        </p>
      </div>

      <!-- Note -->
      <p class="text-center text-sm text-muted mt-12">
        所有订阅方案均为连续包月，可随时取消 · 首月优惠仅限新用户
      </p>
    </div>
  </section>
</template>
