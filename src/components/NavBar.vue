<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const navLinks = [
  { label: '服务', href: '#services' },
  { label: '流程', href: '#flow' },
  { label: '定价', href: '#pricing' },
  { label: '评价', href: '#reviews' },
  { label: 'FAQ', href: '#faq' },
]

function handleScroll() {
  scrolled.value = window.scrollY > 20
}

function closeMenu() {
  menuOpen.value = false
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="scrolled ? 'bg-cream/80 backdrop-blur-lg border-b border-border-warm' : 'bg-transparent'"
  >
    <nav class="max-w-6xl mx-auto px-6 lg:px-8 flex items-center justify-between h-16">
      <!-- Logo -->
      <a href="#" class="flex items-center gap-2 group" @click="closeMenu">
        <div class="w-8 h-8 rounded-lg bg-ink flex items-center justify-center transition-transform group-hover:scale-105">
          <span class="text-cream font-bold text-lg leading-none">C</span>
        </div>
        <span class="font-semibold text-lg tracking-tight text-ink">Curio</span>
      </a>

      <!-- Desktop Nav -->
      <div class="hidden md:flex items-center gap-8">
        <a
          v-for="link in navLinks"
          :key="link.href"
          :href="link.href"
          class="text-sm text-ink-soft hover:text-coral transition-colors duration-200"
        >
          {{ link.label }}
        </a>
      </div>

      <!-- CTA -->
      <div class="hidden md:flex items-center gap-3">
        <a href="#pricing" class="px-4 py-2 text-sm font-medium text-ink hover:text-coral transition-colors">
          登录
        </a>
        <a
          href="#pricing"
          class="px-5 py-2 text-sm font-medium bg-ink text-cream rounded-full hover:bg-coral transition-all duration-300 hover:shadow-lg hover:shadow-coral/20"
        >
          立即开始
        </a>
      </div>

      <!-- Mobile toggle -->
      <button
        class="md:hidden flex flex-col gap-1.5 p-2"
        @click="menuOpen = !menuOpen"
        aria-label="菜单"
      >
        <span class="block w-5 h-0.5 bg-ink transition-all duration-300" :class="menuOpen ? 'rotate-45 translate-y-2' : ''"></span>
        <span class="block w-5 h-0.5 bg-ink transition-all duration-300" :class="menuOpen ? 'opacity-0' : ''"></span>
        <span class="block w-5 h-0.5 bg-ink transition-all duration-300" :class="menuOpen ? '-rotate-45 -translate-y-2' : ''"></span>
      </button>
    </nav>

    <!-- Mobile menu -->
    <transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-2"
      leave-active-class="transition-all duration-200 ease-in"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <div v-if="menuOpen" class="md:hidden bg-cream/95 backdrop-blur-lg border-b border-border-warm">
        <div class="px-6 py-4 flex flex-col gap-4">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="text-base text-ink-soft hover:text-coral transition-colors py-1"
            @click="closeMenu"
          >
            {{ link.label }}
          </a>
          <a
            href="#pricing"
            class="px-5 py-2.5 text-sm font-medium bg-ink text-cream rounded-full text-center"
            @click="closeMenu"
          >
            立即开始
          </a>
        </div>
      </div>
    </transition>
  </header>
</template>
