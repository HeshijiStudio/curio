<script setup lang="ts">
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import ServicesSection from './components/ServicesSection.vue'
import FlowSection from './components/FlowSection.vue'
import PricingSection from './components/PricingSection.vue'
import FAQSection from './components/FAQSection.vue'
import CTASection from './components/CTASection.vue'
import SiteFooter from './components/SiteFooter.vue'
</script>

<template>
  <div class="min-h-screen bg-cream text-ink overflow-x-hidden">
    <NavBar />
    <main>
      <HeroSection />
      <ServicesSection />
      <FlowSection />
      <PricingSection />
      <FAQSection />
      <CTASection />
    </main>
    <SiteFooter />
  </div>
</template>
