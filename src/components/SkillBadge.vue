<script>
export default {
  name: 'SkillBadge',
  props: {
    icon: { type: String, required: true },
    name: { type: String, required: true },
    level: { type: String, default: '' },
  },
}
</script>

<template>
  <div class="flex items-center gap-3 rounded-lg bg-white px-4 py-3 shadow-sm dark:bg-slate-800">
    <span class="text-2xl">{{ icon }}</span>
    <div class="flex flex-col">
      <span class="font-medium text-slate-700 dark:text-slate-200">{{ name }}</span>
      <span v-if="level" class="text-xs text-slate-400 dark:text-slate-500">{{ level }}</span>
    </div>
  </div>
</template>
