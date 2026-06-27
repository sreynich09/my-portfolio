<script>
import SkillBadge from '@/components/SkillBadge.vue'

export default {
  name: 'AboutView',
  components: {
    SkillBadge,
  },
  data() {
    return {
      skills: [
        { name: 'HTML5', icon: '🌐', level: 'Advanced' },
        { name: 'CSS3', icon: '🎨', level: 'Advanced' },
        { name: 'JavaScript', icon: '⚡', level: 'Intermediate' },
        { name: 'Vue.js', icon: '💚', level: 'Intermediate' },
        { name: 'Tailwind CSS', icon: '🌊', level: 'Intermediate' },
        { name: 'Git', icon: '📚', level: 'Beginner' },
      ],
    }
  },
}
</script>

<template>
  <section class="mx-auto max-w-3xl px-4 py-16">
    <h1 class="mb-6 text-4xl font-bold text-slate-800 dark:text-slate-100">About Me</h1>

    <p class="mb-8 leading-relaxed text-slate-600 dark:text-slate-300">
      I am learning web development in a full-stack bootcamp. I enjoy building websites with
      Vue.js.
    </p>

    <h2 class="mb-4 text-2xl font-semibold text-slate-800 dark:text-slate-100">Skills</h2>
    <div class="mb-10 grid grid-cols-2 gap-3 sm:grid-cols-3">
      <SkillBadge
        v-for="skill in skills"
        :key="skill.name"
        :icon="skill.icon"
        :name="skill.name"
        :level="skill.level"
      />
    </div>

    <h2 class="mb-4 text-2xl font-semibold text-slate-800 dark:text-slate-100">Education</h2>
    <p class="text-slate-600 dark:text-slate-300">Full-Stack Web Development Bootcamp — 2026</p>
  </section>
</template>
