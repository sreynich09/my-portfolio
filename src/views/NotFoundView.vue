<script>
export default {
  name: 'NotFoundView',
}
</script>

<template>
  <section class="flex min-h-[70vh] flex-col items-center justify-center px-4 text-center">
    <h1 class="text-gradient text-8xl font-extrabold tracking-tight sm:text-9xl">404</h1>
    <h2 class="mt-4 text-2xl font-bold sm:text-3xl">Page Not Found</h2>
    <p class="mt-3 mb-8 text-slate-500 dark:text-slate-400">
      The page you're looking for doesn't exist.
    </p>
    <RouterLink
      to="/"
      class="rounded-xl bg-gradient-to-r from-indigo-600 to-violet-600 px-7 py-3.5 font-semibold text-white shadow-lg shadow-indigo-500/30 transition hover:-translate-y-0.5"
    >
      ← Go Home
    </RouterLink>
  </section>
</template>
