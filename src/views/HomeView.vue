<script setup></script>

<template>
  <section class="flex min-h-[80vh] flex-col items-center justify-center gap-6 px-4 text-center">
    <h1 class="text-5xl font-bold text-slate-800 sm:text-6xl">
      Hi, I'm <span class="text-indigo-600">Sreynich</span>
    </h1>
    <p class="text-xl text-slate-500">Frontend Developer · Building clean, useful web apps</p>
    <p class="max-w-xl text-slate-600">
      I'm a developer who loves turning ideas into interactive, responsive applications.
    </p>
    <RouterLink
      to="/projects"
      class="rounded-lg bg-indigo-600 px-6 py-3 font-semibold text-white transition hover:bg-indigo-700"
    >
      View Projects
    </RouterLink>
  </section>
</template>
