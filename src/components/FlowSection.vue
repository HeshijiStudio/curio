<script setup lang="ts">
const steps = [
  {
    num: '01',
    title: '父母下单',
    desc: '父母拨打专属电话或微信语音，说出需求即可下单，无需操作 App。',
    icon: 'order',
    color: 'coral',
  },
  {
    num: '02',
    title: '子女接单',
    desc: '子女端收到订单通知，确认需求详情，约定上门时间。',
    icon: 'confirm',
    color: 'amber',
  },
  {
    num: '03',
    title: '上门服务',
    desc: '按时到达，贴心完成服务，全程拍照反馈。',
    icon: 'service',
    color: 'teal',
  },
  {
    num: '04',
    title: '完成确认',
    desc: '服务完成后拍照反馈，子女确认，订单完结。',
    icon: 'done',
    color: 'coral',
  },
]
</script>

<template>
  <section id="flow" class="py-24 lg:py-32 bg-cream-dark/50 relative">
    <div class="max-w-6xl mx-auto px-6 lg:px-8">
      <!-- Section header -->
      <div class="max-w-2xl mb-16">
        <div class="flex items-center gap-3 mb-4">
          <span class="font-mono text-xs text-muted">02</span>
          <div class="w-8 h-px bg-border-warm"></div>
          <span class="text-xs text-muted uppercase tracking-wider">流程</span>
        </div>
        <h2 class="text-3xl md:text-4xl lg:text-5xl font-bold tracking-tight text-ink leading-tight mb-4">
          四步完成，<br />简单高效
        </h2>
        <p class="text-lg text-ink-soft leading-relaxed">
          父母一个电话，子女接单跑腿。全程透明可控，安心省心。
        </p>
      </div>

      <!-- Steps -->
      <div class="relative">
        <!-- Connecting line -->
        <div class="hidden lg:block absolute top-12 left-0 right-0 h-px bg-gradient-to-r from-coral/20 via-amber/20 to-teal/20"></div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8 lg:gap-4 relative">
          <div
            v-for="(step, i) in steps"
            :key="step.num"
            class="relative"
          >
            <!-- Step circle -->
            <div class="relative flex items-center justify-center w-24 h-24 mx-auto mb-6">
              <div
                class="absolute inset-0 rounded-full opacity-10"
                :class="{
                  'bg-coral': step.color === 'coral',
                  'bg-amber': step.color === 'amber',
                  'bg-teal': step.color === 'teal',
                }"
              ></div>
              <div
                class="relative w-16 h-16 rounded-full flex items-center justify-center bg-white border-2 transition-transform hover:scale-105"
                :class="{
                  'border-coral/30': step.color === 'coral',
                  'border-amber/30': step.color === 'amber',
                  'border-teal/30': step.color === 'teal',
                }"
              >
                <!-- Order icon -->
                <svg v-if="step.icon === 'order'" class="w-7 h-7 text-coral" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
                <!-- Confirm icon -->
                <svg v-else-if="step.icon === 'confirm'" class="w-7 h-7 text-amber" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                </svg>
                <!-- Service icon -->
                <svg v-else-if="step.icon === 'service'" class="w-7 h-7 text-teal" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" />
                </svg>
                <!-- Done icon -->
                <svg v-else class="w-7 h-7 text-coral" fill="none" stroke="currentColor" stroke-width="1.8" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <!-- Arrow between steps (desktop) -->
              <svg v-if="i < steps.length - 1" class="hidden lg:block absolute -right-2 top-1/2 -translate-y-1/2 w-4 h-4 text-border-warm" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 5l7 7-7 7" />
              </svg>
            </div>

            <!-- Step content -->
            <div class="text-center">
              <span class="font-mono text-xs text-muted block mb-2">{{ step.num }}</span>
              <h3 class="text-lg font-semibold text-ink mb-2">{{ step.title }}</h3>
              <p class="text-sm text-ink-soft leading-relaxed max-w-[200px] mx-auto">{{ step.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
