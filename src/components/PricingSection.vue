<script setup lang="ts">
import { ref } from 'vue'

const billing = ref<'subscription' | 'single'>('subscription')
const activeProduct = ref(0)

const products = [
  {
    name: '代买',
    fullName: 'Curio 代买',
    subtitle: '菜场超市 · 代买代购',
    icon: 'shopping',
    color: 'coral',
    single: 1,
    tiers: [
      { name: 'Basic', monthly: 7.9, firstMonth: 3.9, count: '8 次/月', perUse: '0.99', features: ['菜市场代买', '超市代购', '30分钟响应'] },
      { name: 'Standard', monthly: 17.9, firstMonth: 8.9, count: '20 次/月', perUse: '0.90', popular: true, features: ['Basic 全部权益', '日用品采购', '药品代买', '优先接单'] },
      { name: 'Pro', monthly: 29.9, firstMonth: 14.9, count: '35 次/月', perUse: '0.85', features: ['Standard 全部权益', '不限品类', '指定时间段', '专属对接'] },
    ],
  },
  {
    name: '代取',
    fullName: 'Curio 代取',
    subtitle: '快递物品 · 代取代送',
    icon: 'package',
    color: 'amber',
    single: 0.5,
    tiers: [
      { name: 'Basic', monthly: 5.9, firstMonth: 2.9, count: '12 次/月', perUse: '0.49', features: ['快递代取', '物品代送', '30分钟响应'] },
      { name: 'Standard', monthly: 11.9, firstMonth: 5.9, count: '25 次/月', perUse: '0.48', popular: true, features: ['Basic 全部权益', '代寄快递', '大件搬运', '优先接单'] },
      { name: 'Pro', monthly: 17.9, firstMonth: 8.9, count: '40 次/月', perUse: '0.45', features: ['Standard 全部权益', '不限重量', '指定时间段', '专属对接'] },
    ],
  },
  {
    name: '家政',
    fullName: 'Curio 家政',
    subtitle: '清洁收纳 · 居家打理',
    icon: 'broom',
    color: 'teal',
    single: 2,
    tiers: [
      { name: 'Basic', monthly: 7.9, firstMonth: 3.9, count: '4 次/月', perUse: '1.98', features: ['基础清洁', '地面打扫', '垃圾清理'] },
      { name: 'Standard', monthly: 14.9, firstMonth: 7.4, count: '8 次/月', perUse: '1.86', popular: true, features: ['Basic 全部权益', '收纳整理', '衣物洗晒', '玻璃擦拭'] },
      { name: 'Pro', monthly: 21.9, firstMonth: 10.9, count: '12 次/月', perUse: '1.83', features: ['Standard 全部权益', '深度清洁', '厨房油烟处理', '专属对接'] },
    ],
  },
  {
    name: '网管',
    fullName: 'Curio 网管',
    subtitle: '网络检测 · 电脑手机维修',
    icon: 'wrench',
    color: 'teal',
    single: 3,
    tiers: [
      { name: 'Basic', monthly: 8.9, firstMonth: 4.4, count: '3 次/月', perUse: '2.97', features: ['网络测速排障', 'WiFi优化', '手机清理加速'] },
      { name: 'Standard', monthly: 16.9, firstMonth: 8.4, count: '6 次/月', perUse: '2.82', popular: true, features: ['Basic 全部权益', '电脑维修调试', '系统重装', '软件安装'] },
      { name: 'Pro', monthly: 26.9, firstMonth: 13.4, count: '10 次/月', perUse: '2.69', features: ['Standard 全部权益', '路由器配置', '智能家居设置', '远程技术支持'] },
    ],
  },
  {
    name: '陪护',
    fullName: 'Curio 陪护',
    subtitle: '陪同就医 · 健康陪护',
    icon: 'heart',
    color: 'coral',
    single: 4,
    tiers: [
      { name: 'Basic', monthly: 11.9, firstMonth: 5.9, count: '3 次/月 (每次2h)', perUse: '3.97', features: ['陪同就医', '取药送药', '就诊排队'] },
      { name: 'Standard', monthly: 18.9, firstMonth: 9.4, count: '5 次/月 (每次3h)', perUse: '3.78', popular: true, features: ['Basic 全部权益', '健康陪护', '康复陪伴', '就诊记录反馈'] },
      { name: 'Pro', monthly: 28.9, firstMonth: 14.4, count: '8 次/月 (每次4h)', perUse: '3.61', features: ['Standard 全部权益', '半日陪护', '健康报告', '专属对接'] },
    ],
  },
  {
    name: '代办',
    fullName: 'Curio 代办',
    subtitle: '代办手续 · 代缴费',
    icon: 'document',
    color: 'amber',
    single: 1,
    tiers: [
      { name: 'Basic', monthly: 7.9, firstMonth: 3.9, count: '8 次/月', perUse: '0.99', features: ['代缴费', '简单跑腿', '30分钟响应'] },
      { name: 'Standard', monthly: 13.9, firstMonth: 6.9, count: '15 次/月', perUse: '0.93', popular: true, features: ['Basic 全部权益', '代办手续', '银行办事', '优先接单'] },
      { name: 'Pro', monthly: 22.9, firstMonth: 11.4, count: '25 次/月', perUse: '0.92', features: ['Standard 全部权益', '证件代办', '加急办理', '专属对接'] },
    ],
  },
]

const bundle = {
  name: 'CurioOne',
  tagline: '一次订阅，全部六大产品不限次',
  monthly: 99.9,
  firstMonth: 49.9,
  individualSum: 148.4,
  features: [
    '六大产品全部包含',
    '不限服务次数',
    '优先派单 + 专属跑腿员',
    '每月健康关怀报告',
    '紧急情况 24h 响应',
    '节假日无加价',
    '家属实时查看服务记录',
    '自动续费，不可取消',
  ],
}

const current = ref(products[0])

function selectProduct(i: number) {
  activeProduct.value = i
  current.value = products[i]
}

interface Order {
  id: string
  token: string
  product: string
  tier: string
  price: number
  type: 'subscription' | 'single'
  status: 'pending' | 'settled'
  createdAt: string
}

const orders = ref<Order[]>([])
const showCheckout = ref(false)
const checkoutItem = ref<{ product: string; tier: string; price: number; type: 'subscription' | 'single' } | null>(null)

function generateToken(): string {
  const date = new Date()
  const y = date.getFullYear()
  const m = String(date.getMonth() + 1).padStart(2, '0')
  const d = String(date.getDate()).padStart(2, '0')
  const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789'
  let rand = ''
  for (let i = 0; i < 4; i++) rand += chars[Math.floor(Math.random() * chars.length)]
  return `CR-${y}${m}${d}-${rand}`
}

function checkout(product: string, tier: string, price: number, type: 'subscription' | 'single') {
  checkoutItem.value = { product, tier, price, type }
  showCheckout.value = true
}

function settleOrder() {
  if (!checkoutItem.value) return
  const now = new Date()
  const time = `${now.getFullYear()}-${String(now.getMonth()+1).padStart(2,'0')}-${String(now.getDate()).padStart(2,'0')} ${String(now.getHours()).padStart(2,'0')}:${String(now.getMinutes()).padStart(2,'0')}`
  orders.value.unshift({
    id: String(Date.now()),
    token: generateToken(),
    product: checkoutItem.value.product,
    tier: checkoutItem.value.tier,
    price: checkoutItem.value.price,
    type: checkoutItem.value.type,
    status: 'settled',
    createdAt: time,
  })
  showCheckout.value = false
  checkoutItem.value = null
}

function closeCheckout() {
  showCheckout.value = false
  checkoutItem.value = null
}
</script>

<template>
  <section id="pricing" class="py-24 lg:py-32 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <div class="max-w-2xl mb-12">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">03</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">定价</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">六大产品，<br />三档选择</h2>
        <p class="text-lg text-ink-soft leading-relaxed">单次1元起，订阅更划算。首月半价，连续包月自动续费。</p>
      </div>

      <div class="flex items-center justify-center gap-1 p-1 bg-cream-dark rounded-full w-fit mx-auto mb-8">
        <button class="px-6 py-2 text-sm font-medium rounded-full transition-all duration-300" :class="billing === 'subscription' ? 'bg-ink text-cream shadow-md' : 'text-ink-soft hover:text-ink'" @click="billing = 'subscription'">订阅制</button>
        <button class="px-6 py-2 text-sm font-medium rounded-full transition-all duration-300" :class="billing === 'single' ? 'bg-ink text-cream shadow-md' : 'text-ink-soft hover:text-ink'" @click="billing = 'single'">单次付费</button>
      </div>

      <div v-if="billing === 'subscription'">
        <div class="flex flex-wrap items-center justify-center gap-2 mb-10">
          <button v-for="(p, i) in products" :key="p.name" class="px-4 py-2 text-sm font-medium rounded-full border transition-all duration-300" :class="activeProduct === i ? 'bg-ink text-cream border-ink' : 'bg-white text-ink-soft border-border-warm hover:border-coral/40'" @click="selectProduct(i)">{{ p.fullName }}</button>
        </div>

        <transition mode="out-in" enter-active-class="transition-all duration-300 ease-out" enter-from-class="opacity-0 translate-y-2" leave-active-class="transition-all duration-150 ease-in" leave-to-class="opacity-0 -translate-y-2">
          <div :key="activeProduct" class="grid md:grid-cols-3 gap-6 mb-12">
            <div v-for="tier in current.tiers" :key="tier.name" class="relative bg-white rounded-2xl border p-8 transition-all duration-300 hover:shadow-xl hover:shadow-ink/5" :class="tier.popular ? 'border-coral/40 shadow-lg ring-1 ring-coral/10 md:scale-105' : 'border-border-warm'">
              <div v-if="tier.popular" class="absolute -top-3 left-1/2 -translate-x-1/2"><span class="px-4 py-1 bg-coral text-cream text-xs font-medium rounded-full">最受欢迎</span></div>
              <div class="mb-5">
                <h3 class="text-lg font-semibold text-ink mb-1">{{ current.fullName }} · {{ tier.name }}</h3>
                <p class="text-sm text-muted">{{ current.subtitle }}</p>
              </div>
              <div class="mb-1">
                <div class="flex items-baseline gap-1"><span class="text-4xl font-bold text-ink">¥{{ tier.firstMonth }}</span><span class="text-sm text-muted">/ 首月</span></div>
                <div class="flex items-center gap-2 mt-1"><p class="text-xs text-coral">次月 ¥{{ tier.monthly }}/月</p><span class="text-muted">·</span><p class="text-xs text-muted">{{ tier.count }}</p></div>
                <p class="text-xs text-teal mt-1.5 font-medium">约 ¥{{ tier.perUse }}/次</p>
              </div>
              <div class="my-6 h-px bg-border-warm"></div>
              <ul class="space-y-3 mb-8">
                <li v-for="feature in tier.features" :key="feature" class="flex items-center gap-2.5 text-sm text-ink-soft">
                  <svg class="w-4 h-4 flex-shrink-0" :class="{ 'text-coral': current.color === 'coral', 'text-teal': current.color === 'teal', 'text-amber': current.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>
                  {{ feature }}
                </li>
              </ul>
              <button class="block w-full py-3 text-center font-medium rounded-full transition-all duration-300 cursor-pointer" :class="tier.popular ? 'bg-ink text-cream hover:bg-coral' : 'bg-cream-dark text-ink hover:bg-border-warm'" @click="checkout(current.fullName, tier.name, tier.monthly, 'subscription')">去结算</button>
            </div>
          </div>
        </transition>

        <div class="max-w-2xl mx-auto bg-cream-dark/60 rounded-2xl p-6 mb-12 flex items-center justify-between">
          <div><p class="text-sm text-muted mb-1">不想订阅？</p><p class="text-sm text-ink-soft">{{ current.fullName }} 也支持单次付费</p></div>
          <div class="text-right"><span class="text-2xl font-bold text-ink">¥{{ current.single }}</span><span class="text-sm text-muted">/ 次</span><button class="ml-4 text-sm text-coral hover:underline" @click="billing = 'single'">查看单次 →</button></div>
        </div>

        <div class="relative bg-gradient-to-br from-ink to-ink-soft rounded-3xl p-8 lg:p-12 overflow-hidden">
          <div class="absolute top-0 right-0 w-96 h-96 bg-coral/10 rounded-full blur-3xl -translate-y-1/2 translate-x-1/4"></div>
          <div class="absolute bottom-0 left-0 w-64 h-64 bg-teal/10 rounded-full blur-3xl translate-y-1/2"></div>
          <div class="relative grid lg:grid-cols-2 gap-8 lg:gap-12 items-center">
            <div>
              <div class="inline-flex items-center gap-2 px-3 py-1 bg-coral/20 border border-coral/30 rounded-full mb-6"><svg class="w-3.5 h-3.5 text-coral-light" fill="currentColor" viewBox="0 0 20 20"><path d="M10 15l-5.878 3.09 1.123-6.545L.49 6.91l6.572-.955L10 0l2.938 5.955 6.572.955-4.755 4.635 1.123 6.545z"/></svg><span class="text-xs text-coral-light font-medium">最超值 · 省钱之选</span></div>
              <h3 class="text-2xl lg:text-3xl font-bold text-cream mb-3">{{ bundle.name }}</h3>
              <p class="text-cream/60 text-base mb-8">{{ bundle.tagline }}</p>
              <div class="flex items-baseline gap-2 mb-2"><span class="text-5xl font-bold text-cream">¥{{ bundle.firstMonth }}</span><span class="text-cream/50 text-sm">/ 首月</span></div>
              <p class="text-coral-light text-sm">次月 ¥{{ bundle.monthly }}/月 · 自动续费</p>
              <div class="mt-4 inline-flex items-center gap-2 px-3 py-1.5 bg-teal/20 border border-teal/30 rounded-lg"><svg class="w-4 h-4 text-teal-light" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" /></svg><span class="text-sm text-teal-light font-medium">较单独订阅全部 Pro 省 ¥{{ (bundle.individualSum - bundle.monthly).toFixed(1) }} / 月</span></div>
            </div>
            <div>
              <ul class="grid grid-cols-1 sm:grid-cols-2 gap-3 mb-8">
                <li v-for="feature in bundle.features" :key="feature" class="flex items-start gap-2.5 text-sm text-cream/80"><svg class="w-4 h-4 text-coral-light flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" /></svg>{{ feature }}</li>
              </ul>
              <button @click="checkout('CurioOne', 'All-in-One', bundle.monthly, 'subscription')" class="inline-flex items-center gap-2 px-8 py-3.5 bg-coral text-cream font-medium rounded-full hover:bg-coral-dark transition-all duration-300 hover:shadow-xl hover:shadow-coral/30 cursor-pointer">去结算<svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" /></svg></button>
            </div>
          </div>
        </div>
      </div>

      <div v-else class="max-w-4xl mx-auto">
        <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
          <div v-for="p in products" :key="p.name" class="bg-white rounded-2xl border border-border-warm p-6 text-center hover:shadow-lg hover:shadow-ink/5 transition-all duration-300">
            <div class="w-12 h-12 rounded-xl flex items-center justify-center mx-auto mb-4" :class="{ 'bg-coral-light': p.color === 'coral', 'bg-teal-light': p.color === 'teal', 'bg-amber-light': p.color === 'amber' }">
              <svg v-if="p.icon === 'shopping'" class="w-6 h-6" :class="{ 'text-coral': p.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
              <svg v-else-if="p.icon === 'package'" class="w-6 h-6" :class="{ 'text-amber': p.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
              <svg v-else-if="p.icon === 'broom'" class="w-6 h-6" :class="{ 'text-teal': p.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.324.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 011.37.49l1.296 2.247a1.125 1.125 0 01-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 010 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 01-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 01-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 01-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 01-1.369-.49l-1.297-2.247a1.125 1.125 0 01.26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 010-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 01-.26-1.43l1.297-2.247a1.125 1.125 0 011.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28 z" /><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
              <svg v-else-if="p.icon === 'wrench'" class="w-6 h-6" :class="{ 'text-teal': p.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
              <svg v-else-if="p.icon === 'heart'" class="w-6 h-6" :class="{ 'text-coral': p.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
              <svg v-else class="w-6 h-6" :class="{ 'text-amber': p.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 002.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 00-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25z" /></svg>
            </div>
            <h3 class="text-sm font-semibold text-ink mb-1">{{ p.fullName }}</h3>
            <p class="text-xs text-muted mb-3">{{ p.subtitle }}</p>
            <div class="flex items-baseline justify-center gap-0.5 mb-4"><span class="text-3xl font-bold text-ink">¥{{ p.single }}</span><span class="text-xs text-muted">/次</span></div>
            <button @click="checkout(p.fullName, '单次', p.single, 'single')" class="w-full py-2 text-sm font-medium rounded-full bg-cream-dark text-ink hover:bg-border-warm transition-all duration-300 cursor-pointer">去结算</button>
          </div>
        </div>
        <p class="text-center text-sm text-muted mt-8">经常需要服务？<button class="text-coral hover:underline" @click="billing = 'subscription'">看看订阅方案 →</button></p>
      </div>

      <p class="text-center text-sm text-muted mt-12">所有订阅方案均为连续包月，自动续费，订阅生效后不可取消 · 首月优惠仅限新用户</p>

      <!-- Checkout inline card -->
      <transition enter-active-class="transition-all duration-400 ease-out" enter-from-class="opacity-0 max-h-0" enter-to-class="opacity-100 max-h-[600px]" leave-active-class="transition-all duration-300 ease-in" leave-from-class="opacity-100 max-h-[600px]" leave-to-class="opacity-0 max-h-0">
        <div v-if="showCheckout && checkoutItem" class="mt-12 overflow-hidden">
          <div class="max-w-lg mx-auto bg-white rounded-2xl border-2 border-coral/30 shadow-xl shadow-coral/10 p-8">
            <div class="flex items-center justify-between mb-6">
              <h3 class="text-lg font-semibold text-ink">确认订单</h3>
              <button @click="closeCheckout" class="w-8 h-8 flex items-center justify-center rounded-full hover:bg-cream-dark transition-colors"><svg class="w-4 h-4 text-muted" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" /></svg></button>
            </div>
            <div class="space-y-4 mb-6">
              <div class="flex justify-between text-sm"><span class="text-ink-soft">产品</span><span class="text-ink font-medium">{{ checkoutItem.product }}</span></div>
              <div class="flex justify-between text-sm"><span class="text-ink-soft">档位</span><span class="text-ink font-medium">{{ checkoutItem.tier }}</span></div>
              <div class="flex justify-between text-sm"><span class="text-ink-soft">类型</span><span class="text-ink font-medium">{{ checkoutItem.type === 'subscription' ? '订阅制 · 自动续费' : '单次付费' }}</span></div>
              <div class="h-px bg-border-warm"></div>
              <div class="flex justify-between"><span class="text-ink-soft">应付金额</span><span class="text-xl font-bold text-ink">¥{{ checkoutItem.price }}<span class="text-xs text-muted font-normal">{{ checkoutItem.type === 'subscription' ? '/月' : '' }}</span></span></div>
            </div>
            <button @click="settleOrder" class="w-full py-3.5 bg-ink text-cream font-medium rounded-full hover:bg-coral transition-all duration-300 cursor-pointer">已结算</button>
            <p class="text-xs text-muted text-center mt-3">点击确认即视为已结算，订阅生效后不可取消</p>
          </div>
        </div>
      </transition>

      <!-- Order work tickets -->
      <div v-if="orders.length > 0" class="mt-12">
        <h3 class="text-lg font-semibold text-ink mb-4">我的工单</h3>
        <div class="space-y-3">
          <div v-for="order in orders" :key="order.id" class="bg-white rounded-xl border border-border-warm p-6 hover:shadow-md transition-all duration-300">
            <div class="flex items-start justify-between mb-3">
              <div><p class="text-sm font-medium text-ink">{{ order.product }} · {{ order.tier }}</p><p class="text-xs text-muted mt-0.5">{{ order.createdAt }}</p></div>
              <span class="px-3 py-1 text-xs font-medium rounded-full" :class="order.status === 'settled' ? 'bg-teal-light text-teal' : 'bg-amber-light text-amber'">{{ order.status === 'settled' ? '已结算' : '待结算' }}</span>
            </div>
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2"><span class="text-xs text-muted">Token</span><code class="px-2 py-0.5 bg-cream-dark text-ink text-xs font-mono rounded">{{ order.token }}</code></div>
              <span class="text-sm font-semibold text-ink">¥{{ order.price }}{{ order.type === 'subscription' ? '/月' : '' }}</span>
            </div>
            <div class="mt-3 pt-3 border-t border-border-warm"><p class="text-xs text-ink-soft">{{ order.type === 'subscription' ? '订阅制 · 自动续费 · 不可取消' : '单次付费 · 即用即付' }}</p></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
