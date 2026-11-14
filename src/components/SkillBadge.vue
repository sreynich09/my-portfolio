<script>
export default {
  name: 'SkillBadge',
  props: {
    icon: { type: String, required: true },
    name: { type: String, required: true },
    level: { type: String, default: '' },
  },
  computed: {
    levelClass() {
      return {
        Professional: 'bg-violet-100 text-violet-700 dark:bg-violet-500/15 dark:text-violet-300',
        Advanced: 'bg-emerald-100 text-emerald-700 dark:bg-emerald-500/15 dark:text-emerald-300',
        Intermediate: 'bg-indigo-100 text-indigo-700 dark:bg-indigo-500/15 dark:text-indigo-300',
        Beginner: 'bg-amber-100 text-amber-700 dark:bg-amber-500/15 dark:text-amber-300',
      }[this.level] || 'bg-slate-100 text-slate-600 dark:bg-slate-800 dark:text-slate-300'
    },
  },
}
</script>

<template>
  <div
    class="group flex items-center gap-3 rounded-2xl border border-slate-200 bg-white p-4 transition hover:-translate-y-1 hover:border-indigo-300 hover:shadow-lg hover:shadow-indigo-500/10 dark:border-slate-800 dark:bg-slate-900 dark:hover:border-indigo-500/50"
  >
    <span
      class="grid h-11 w-11 shrink-0 place-items-center rounded-xl bg-slate-100 text-2xl transition group-hover:scale-110 dark:bg-slate-800"
      >{{ icon }}</span
    >
    <div class="flex min-w-0 flex-col items-start gap-1">
      <span class="font-semibold text-slate-800 dark:text-slate-100">{{ name }}</span>
      <span v-if="level" class="rounded-full px-2 py-0.5 text-xs font-medium" :class="levelClass">{{
        level
      }}</span>
    </div>
  </div>
</template>
