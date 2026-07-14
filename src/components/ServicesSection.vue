<script setup lang="ts">
const services = [
  {
    id: '01',
    title: '代买',
    subtitle: '菜场超市，代买代购',
    icon: 'shopping',
    color: 'coral',
    features: ['菜市场代买', '超市代购', '日用品采购', '药品代买'],
    description: '新鲜蔬菜、日常用品、急需药品，一个电话就送到家。',
  },
  {
    id: '02',
    title: '代取',
    subtitle: '快递物品，代取代送',
    icon: 'package',
    color: 'amber',
    features: ['快递代取', '物品代送', '代寄快递', '大件搬运'],
    description: '快递到了没空取？重物需要搬上楼？我们代取代送。',
  },
  {
    id: '03',
    title: '家政',
    subtitle: '清洁收纳，居家打理',
    icon: 'broom',
    color: 'teal',
    features: ['居家清洁', '收纳整理', '衣物洗晒', '玻璃擦拭'],
    description: '定期上门打扫、整理收纳，让父母的居住环境更舒适。',
  },
  {
    id: '04',
    title: '网管',
    subtitle: '网络检测，电脑手机维修',
    icon: 'wrench',
    color: 'teal',
    features: ['网络测速排障', 'WiFi优化', '电脑维修调试', '系统重装'],
    description: '网络不通、电脑卡顿、手机不会用，一个电话远程或上门解决。',
  },
  {
    id: '05',
    title: '陪护',
    subtitle: '陪同就医，健康陪护',
    icon: 'heart',
    color: 'coral',
    features: ['陪同就医', '健康陪护', '取药送药', '康复陪伴'],
    description: '陪同看病、取药送药，让父母就医不再孤单。',
  },
  {
    id: '06',
    title: '代办',
    subtitle: '代办手续，代缴费',
    icon: 'document',
    color: 'amber',
    features: ['代办手续', '代缴费', '银行办事', '证件代办'],
    description: '代办各类手续、代缴费，让父母不再为繁琐事务烦恼。',
  },
]
</script>

<template>
  <section id="services" class="py-24 lg:py-32 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <!-- Section header -->
      <div class="max-w-2xl mb-16">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">01</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">服务</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">
          六大服务，<br />覆盖家长日常所需
        </h2>
        <p class="text-lg text-ink-soft leading-relaxed">
          从柴米油盐到看病就医，我们用专业和温度，照顾父母的每一个日常。
        </p>
      </div>

      <!-- Service cards: 3 columns x 2 rows -->
      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
        <div
          v-for="service in services"
          :key="service.id"
          class="group relative bg-white rounded-2xl border border-border-warm p-8 hover:shadow-xl hover:shadow-ink/5 hover:-translate-y-1 transition-all duration-300"
        >
          <!-- Icon -->
          <div
            class="w-14 h-14 rounded-xl flex items-center justify-center mb-6 transition-transform group-hover:scale-110"
            :class="{
              'bg-coral-light': service.color === 'coral',
              'bg-teal-light': service.color === 'teal',
              'bg-amber-light': service.color === 'amber',
            }"
          >
            <svg v-if="service.icon === 'shopping'" class="w-7 h-7" :class="{ 'text-coral': service.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
            <svg v-else-if="service.icon === 'package'" class="w-7 h-7" :class="{ 'text-amber': service.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" /></svg>
            <svg v-else-if="service.icon === 'broom'" class="w-7 h-7" :class="{ 'text-teal': service.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.594 3.94c.09-.542.56-.94 1.11-.94h2.593c.55 0 1.02.398 1.11.94l.213 1.281c.063.374.313.686.645.87.074.04.147.083.22.127.324.196.72.257 1.075.124l1.217-.456a1.125 1.125 0 011.37.49l1.296 2.247a1.125 1.125 0 01-.26 1.431l-1.003.827c-.293.241-.438.613-.43.992a7.723 7.723 0 010 .255c-.008.378.137.75.43.991l1.004.827c.424.35.534.955.26 1.43l-1.298 2.247a1.125 1.125 0 01-1.369.491l-1.217-.456c-.355-.133-.75-.072-1.076.124a6.47 6.47 0 01-.22.128c-.331.183-.581.495-.644.869l-.213 1.281c-.09.543-.56.94-1.11.94h-2.594c-.55 0-1.019-.398-1.11-.94l-.213-1.281c-.062-.374-.312-.686-.644-.87a6.52 6.52 0 01-.22-.127c-.325-.196-.72-.257-1.076-.124l-1.217.456a1.125 1.125 0 01-1.369-.49l-1.297-2.247a1.125 1.125 0 01.26-1.431l1.004-.827c.292-.24.437-.613.43-.991a6.932 6.932 0 010-.255c.007-.38-.138-.751-.43-.992l-1.004-.827a1.125 1.125 0 01-.26-1.43l1.297-2.247a1.125 1.125 0 011.37-.491l1.216.456c.356.133.751.072 1.076-.124.072-.044.146-.086.22-.128.332-.183.582-.495.644-.869l.214-1.28z" /><path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" /></svg>
            <svg v-else-if="service.icon === 'wrench'" class="w-7 h-7" :class="{ 'text-teal': service.color === 'teal' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9.75 17L9 20l-1 1h8l-1-1-.75-3M3 13h18M5 17h14a2 2 0 002-2V5a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" /></svg>
            <svg v-else-if="service.icon === 'heart'" class="w-7 h-7" :class="{ 'text-coral': service.color === 'coral' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" /></svg>
            <svg v-else class="w-7 h-7" :class="{ 'text-amber': service.color === 'amber' }" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 002.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 00-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 00.75-.75 2.25 2.25 0 00-.1-.664m-5.8 0A2.251 2.251 0 0113.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25z" /></svg>
          </div>

          <!-- Content -->
          <div class="flex items-baseline gap-2 mb-1">
            <span class="font-mono text-xs text-muted">{{ service.id }}</span>
            <h3 class="text-xl font-semibold text-ink">{{ service.title }}</h3>
          </div>
          <p class="text-sm text-coral mb-3">{{ service.subtitle }}</p>
          <p class="text-sm text-ink-soft leading-relaxed mb-6">{{ service.description }}</p>

          <!-- Features -->
          <ul class="space-y-2.5">
            <li v-for="feature in service.features" :key="feature" class="flex items-center gap-2.5 text-sm text-ink-soft">
              <svg
                class="w-4 h-4 flex-shrink-0"
                :class="{ 'text-coral': service.color === 'coral', 'text-teal': service.color === 'teal', 'text-amber': service.color === 'amber' }"
                fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
              </svg>
              {{ feature }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
