<script>
export default {
  name: 'ProjectCard',
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
}
</script>

<template>
  <article
    class="group relative flex flex-col overflow-hidden rounded-2xl border border-slate-200 bg-white transition duration-300 hover:-translate-y-2 hover:border-indigo-300 hover:shadow-2xl hover:shadow-indigo-500/15 dark:border-slate-800 dark:bg-slate-900 dark:hover:border-indigo-500/50"
  >
    <div
      class="relative grid h-40 place-items-center overflow-hidden bg-gradient-to-br from-indigo-100 via-violet-100 to-fuchsia-100 dark:from-indigo-500/20 dark:via-violet-500/15 dark:to-fuchsia-500/20"
    >
      <img
        v-if="project.image"
        :src="project.image"
        :alt="`${project.title} screenshot`"
        loading="lazy"
        class="h-full w-full object-cover object-top transition duration-500 group-hover:scale-105"
      />
      <span
        v-else
        class="text-6xl transition duration-300 group-hover:scale-125 group-hover:-rotate-6"
      >
        {{ project.emoji }}
      </span>
    </div>

    <div class="flex flex-1 flex-col p-6">
      <h3 class="mb-2 text-xl font-bold text-slate-800 dark:text-slate-100">{{ project.title }}</h3>
      <p class="mb-5 flex-1 leading-relaxed text-slate-500 dark:text-slate-400">
        {{ project.description }}
      </p>
      <div class="flex flex-wrap gap-2">
        <span
          v-for="tech in project.technologies"
          :key="tech"
          class="rounded-full bg-indigo-50 px-3 py-1 text-xs font-medium text-indigo-700 dark:bg-indigo-500/15 dark:text-indigo-300"
        >
          {{ tech }}
        </span>
      </div>
      <div
        v-if="project.github || project.demo"
        class="mt-5 flex gap-3 border-t border-slate-100 pt-4 dark:border-slate-800"
      >
        <a
          v-if="project.github"
          :href="project.github"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-1.5 text-sm font-semibold text-slate-700 transition hover:text-indigo-600 dark:text-slate-200 dark:hover:text-indigo-300"
        >
          <svg viewBox="0 0 24 24" class="h-4 w-4" fill="currentColor" aria-hidden="true">
            <path
              d="M12 .5C5.65.5.5 5.65.5 12a11.5 11.5 0 0 0 7.86 10.92c.58.1.79-.25.79-.56v-2c-3.2.7-3.87-1.37-3.87-1.37-.52-1.33-1.28-1.69-1.28-1.69-1.05-.72.08-.7.08-.7 1.16.08 1.77 1.19 1.77 1.19 1.03 1.77 2.7 1.26 3.36.96.1-.75.4-1.26.73-1.55-2.55-.29-5.24-1.28-5.24-5.69 0-1.26.45-2.29 1.19-3.1-.12-.29-.52-1.46.11-3.05 0 0 .97-.31 3.18 1.18a11 11 0 0 1 5.79 0c2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.23 2.76.11 3.05.74.81 1.19 1.84 1.19 3.1 0 4.42-2.7 5.4-5.26 5.68.41.36.78 1.06.78 2.14v3.17c0 .31.21.67.8.56A11.5 11.5 0 0 0 23.5 12C23.5 5.65 18.35.5 12 .5Z"
            />
          </svg>
          Code
        </a>
        <a
          v-if="project.demo"
          :href="project.demo"
          target="_blank"
          rel="noopener noreferrer"
          class="inline-flex items-center gap-1.5 text-sm font-semibold text-indigo-600 transition hover:text-indigo-700 dark:text-indigo-300"
        >
          Live demo ↗
        </a>
      </div>
    </div>
  </article>
</template>
