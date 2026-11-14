<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'

const isDark = ref(false)
onMounted(() => {
  isDark.value = document.documentElement.classList.contains('dark')
})

function toggleTheme() {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
  try {
    localStorage.setItem('theme', isDark.value ? 'dark' : 'light')
  } catch {
    // storage unavailable – theme just won't persist
  }
}

const isOpen = ref(false)
const route = useRoute()
watch(() => route.path, () => (isOpen.value = false))

const links = [
  { to: '/', label: 'Home' },
  { to: '/about', label: 'About' },
  { to: '/projects', label: 'Projects' },
  { to: '/contact', label: 'Contact' },
]
const year = new Date().getFullYear()
</script>

<template>
  <div class="flex min-h-screen flex-col page-fade-in">
    <nav
      class="sticky top-0 z-50 border-b border-slate-200/70 bg-white/70 backdrop-blur-lg dark:border-slate-800/70 dark:bg-slate-950/70"
    >
      <div class="mx-auto flex max-w-6xl items-center justify-between px-4 py-3 sm:px-6">
        <RouterLink to="/" class="flex items-center gap-2 text-lg font-bold tracking-tight">
          <span
            class="grid h-9 w-9 place-items-center rounded-xl bg-gradient-to-br from-indigo-500 to-fuchsia-500 text-white shadow-md shadow-indigo-500/30"
            >S</span
          >
          <span>Morn Sreynich</span>
        </RouterLink>

        <div class="flex items-center gap-2">
          <!-- Desktop links -->
          <div class="hidden items-center gap-1 md:flex">
            <RouterLink
              v-for="link in links"
              :key="link.to"
              :to="link.to"
              class="rounded-full px-4 py-2 text-sm font-medium text-slate-600 transition hover:bg-slate-100 hover:text-slate-900 dark:text-slate-300 dark:hover:bg-slate-800 dark:hover:text-white"
              exact-active-class="!bg-indigo-50 !text-indigo-600 dark:!bg-indigo-500/15 dark:!text-indigo-300"
            >
              {{ link.label }}
            </RouterLink>
          </div>

          <button
            @click="toggleTheme"
            class="grid h-10 w-10 place-items-center rounded-full text-lg transition hover:bg-slate-100 dark:hover:bg-slate-800"
            :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
          >
            {{ isDark ? '☀️' : '🌙' }}
          </button>

          <!-- Mobile toggle -->
          <button
            class="grid h-10 w-10 place-items-center rounded-full text-xl transition hover:bg-slate-100 md:hidden dark:hover:bg-slate-800"
            :aria-expanded="isOpen"
            aria-label="Toggle menu"
            @click="isOpen = !isOpen"
          >
            {{ isOpen ? '✕' : '☰' }}
          </button>
        </div>
      </div>

      <!-- Mobile menu -->
      <div v-if="isOpen" class="flex flex-col gap-1 px-4 pb-4 md:hidden">
        <RouterLink
          v-for="link in links"
          :key="link.to"
          :to="link.to"
          class="rounded-xl px-4 py-3 font-medium text-slate-600 hover:bg-slate-100 dark:text-slate-300 dark:hover:bg-slate-800"
          exact-active-class="!bg-indigo-50 !text-indigo-600 dark:!bg-indigo-500/15 dark:!text-indigo-300"
        >
          {{ link.label }}
        </RouterLink>
      </div>
    </nav>

    <main class="flex-1">
      <RouterView v-slot="{ Component }">
        <Transition name="route-fade" mode="out-in">
          <component :is="Component" />
        </Transition>
      </RouterView>
    </main>

    <footer class="border-t border-slate-200 dark:border-slate-800">
      <div
        class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-2 px-4 py-6 text-sm text-slate-500 sm:flex-row sm:px-6 dark:text-slate-400"
      >
        <p>© {{ year }} Morn Sreynich (Nich09). All rights reserved.</p>
        <p>Built with Vue.js &amp; Tailwind CSS</p>
      </div>
    </footer>
  </div>
</template>
