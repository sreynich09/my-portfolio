<script setup>
const stack = ['Web Scraping', 'Data Integration', 'Vue.js', 'JavaScript', 'Tailwind CSS', 'Git']
</script>

<template>
  <section class="relative isolate overflow-hidden">
    <!-- Decorative background -->
    <div class="pointer-events-none absolute inset-0 -z-10">
      <div
        class="animate-float absolute -top-24 left-1/2 h-96 w-96 -translate-x-1/2 rounded-full bg-indigo-400/30 blur-3xl dark:bg-indigo-600/20"
      ></div>
      <div
        class="animate-float absolute top-40 -right-20 h-72 w-72 rounded-full bg-fuchsia-400/25 blur-3xl [animation-delay:-5s] dark:bg-fuchsia-600/15"
      ></div>
      <div
        class="absolute inset-0 bg-[radial-gradient(circle_at_1px_1px,rgb(148_163_184/0.25)_1px,transparent_0)] [background-size:24px_24px] [mask-image:radial-gradient(ellipse_at_center,black_30%,transparent_75%)]"
      ></div>
    </div>

    <div
      class="mx-auto flex min-h-[calc(100vh-8rem)] max-w-4xl flex-col items-center justify-center gap-7 px-4 py-20 text-center"
    >
      <span
        class="inline-flex items-center gap-2 rounded-full border border-indigo-200 bg-white/70 px-4 py-1.5 text-sm font-medium text-indigo-700 backdrop-blur dark:border-indigo-500/30 dark:bg-indigo-500/10 dark:text-indigo-300"
      >
        <span class="relative flex h-2 w-2">
          <span
            class="absolute inline-flex h-full w-full animate-ping rounded-full bg-emerald-400 opacity-75"
          ></span>
          <span class="relative inline-flex h-2 w-2 rounded-full bg-emerald-500"></span>
        </span>
        Open to opportunities
      </span>

      <h1 class="text-5xl font-extrabold tracking-tight sm:text-7xl">
        Hi, I'm <span class="text-gradient">Morn Sreynich</span> 👋
      </h1>

      <p class="text-xl font-medium text-slate-600 sm:text-2xl dark:text-slate-300">
        Software Developer · Based in Cambodia 🇰🇭
      </p>

      <p class="max-w-xl text-lg leading-relaxed text-slate-500 dark:text-slate-400">
        I build and maintain scraping modules that collect data from banks and card companies across
        Japan, Vietnam, the UAE, India, and more — and I'm preparing to start a master's in Data
        Science.
      </p>

      <div class="flex flex-col gap-3 sm:flex-row">
        <RouterLink
          to="/projects"
          class="rounded-xl bg-gradient-to-r from-indigo-600 to-violet-600 px-7 py-3.5 font-semibold text-white shadow-lg shadow-indigo-500/30 transition hover:-translate-y-0.5 hover:shadow-xl hover:shadow-indigo-500/40"
        >
          View Projects →
        </RouterLink>
        <RouterLink
          to="/contact"
          class="rounded-xl border border-slate-300 bg-white/70 px-7 py-3.5 font-semibold text-slate-700 backdrop-blur transition hover:-translate-y-0.5 hover:border-indigo-400 hover:text-indigo-600 dark:border-slate-700 dark:bg-slate-900/70 dark:text-slate-200 dark:hover:border-indigo-400 dark:hover:text-indigo-300"
        >
          Get in Touch
        </RouterLink>
      </div>

      <div class="mt-6 flex flex-wrap justify-center gap-2">
        <span
          v-for="tech in stack"
          :key="tech"
          class="rounded-full bg-slate-100 px-3 py-1 text-sm text-slate-600 dark:bg-slate-800/80 dark:text-slate-300"
        >
          {{ tech }}
        </span>
      </div>
    </div>
  </section>
</template>
