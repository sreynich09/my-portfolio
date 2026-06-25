<script setup>
import { ref } from 'vue'

const isOpen = ref(false)
const links = [
  { to: '/', label: 'Home' },
  { to: '/about', label: 'About' },
  { to: '/projects', label: 'Projects' },
  { to: '/contact', label: 'Contact' },
]
</script>

<template>
  <div class="min-h-screen bg-slate-50 text-slate-800">
    <nav class="sticky top-0 z-50 bg-white shadow-sm">
      <div class="mx-auto flex max-w-6xl items-center justify-between px-4 py-4">
        <RouterLink to="/" class="text-xl font-bold text-indigo-600">Vue Router Learning</RouterLink>

        <!-- Desktop links -->
        <div class="hidden gap-6 md:flex">
          <RouterLink
            v-for="link in links"
            :key="link.to"
            :to="link.to"
            class="font-medium text-slate-600 transition hover:text-indigo-600"
            active-class="text-indigo-600 font-semibold"
          >
            {{ link.label }}
          </RouterLink>
        </div>

        <!-- Mobile toggle -->
        <button class="md:hidden" @click="isOpen = !isOpen">
          <span class="text-2xl">{{ isOpen ? '✕' : '☰' }}</span>
        </button>
      </div>

      <!-- Mobile menu -->
      <div v-if="isOpen" class="flex flex-col gap-4 px-4 pb-4 md:hidden">
        <RouterLink
          v-for="link in links"
          :key="link.to"
          :to="link.to"
          class="font-medium text-slate-600"
          active-class="text-indigo-600 font-semibold"
          @click="isOpen = false"
        >
          {{ link.label }}
        </RouterLink>
      </div>
    </nav>

    <main>
      <RouterView />
    </main>
  </div>
</template>
