<script setup>
import { ref, onMounted} from 'vue'

// Add a toggle button for dark/light mode
const isDark = ref(false)
onMounted(() => {
  const stored = localStorage.getItem('theme')
  isDark.value = stored ? stored === 'dark' : window.matchMedia('(prefers-color-scheme: dark)').matches
  document.documentElement.classList.toggle('dark', isDark.value)
})

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
}

const isOpen = ref(false)
const links = [
  { to: '/', label: 'Home' },
  { to: '/about', label: 'About' },
  { to: '/projects', label: 'Projects' },
  { to: '/contact', label: 'Contact' },
]
</script>

<template>
  <div class="min-h-screen bg-slate-50 text-slate-800 dark:bg-slate-950 dark:text-slate-100 page-fade-in">
    <nav class="sticky top-0 z-50 bg-white shadow-sm dark:bg-slate-900">
      <div class="mx-auto flex max-w-6xl items-center justify-between px-4 py-4">
        <RouterLink to="/" class="text-xl font-bold text-indigo-600">Vue Router Learning</RouterLink>

        <!-- Desktop links -->
        <div class="hidden gap-6 md:flex">
          <RouterLink
            v-for="link in links"
            :key="link.to"
            :to="link.to"
            class="font-medium text-slate-600 transition hover:text-indigo-600 dark:text-slate-300"
            active-class="bg-indigo-200 text-indigo-600 font-semibold rounded-full px-3 py-1 dark:bg-indigo-900"
          >
            {{ link.label }}
          </RouterLink>
        </div>

        <!-- Mobile toggle -->
        <button class="md:hidden" @click="isOpen = !isOpen">
          <span class="text-2xl">{{ isOpen ? '✕' : '☰' }}</span>
        </button>

        <button @click="toggleTheme" class="text-xl" aria-label="Toggle dark mode">
          {{ isDark ? '☀️' : '🌙' }}
        </button>
      </div>

      <!-- Mobile menu -->
      <div v-if="isOpen" class="flex flex-col gap-4 px-4 pb-4 md:hidden">
        <RouterLink
          v-for="link in links"
          :key="link.to"
          :to="link.to"
          class="font-medium text-slate-600 dark:text-slate-300"
          active-class="text-indigo-600 font-semibold"
          @click="isOpen = false"
        >
          {{ link.label }}
        </RouterLink>
      </div>
    </nav>

    <main>
      <RouterView v-slot="{ Component }">
        <Transition name="route-fade" mode="out-in">
          <component :is="Component" />
        </Transition>
      </RouterView>
    </main>
  </div>
</template>
