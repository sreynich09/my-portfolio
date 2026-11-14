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
        { name: 'Web Scraping', icon: '🕷️', level: 'Professional' },
        { name: 'Data Integration', icon: '🔗', level: 'Professional' },
        { name: 'HTML5', icon: '🌐', level: 'Advanced' },
        { name: 'CSS3', icon: '🎨', level: 'Advanced' },
        { name: 'JavaScript', icon: '⚡', level: 'Intermediate' },
        { name: 'Vue.js', icon: '💚', level: 'Intermediate' },
        { name: 'Tailwind CSS', icon: '🌊', level: 'Intermediate' },
        { name: 'Git', icon: '📚', level: 'Beginner' },
      ],
      countries: ['🇯🇵 Japan', '🇻🇳 Vietnam', '🇦🇪 UAE', '🇮🇳 India', '🌏 and more'],
      languages: ['한국어 Korean', '日本語 Japanese', 'English'],
    }
  },
}
</script>

<template>
  <section class="mx-auto max-w-5xl px-4 py-16 sm:px-6 sm:py-24">
    <!-- Intro -->
    <div class="grid items-center gap-10 md:grid-cols-[auto_1fr]">
      <div class="relative mx-auto">
        <div
          class="absolute -inset-1 rounded-[2rem] bg-gradient-to-br from-indigo-500 via-violet-500 to-fuchsia-500 opacity-70 blur-lg"
        ></div>
        <div
          class="relative grid h-44 w-44 place-items-center rounded-[2rem] bg-gradient-to-br from-indigo-500 via-violet-500 to-fuchsia-500 text-7xl font-extrabold text-white"
        >
          S
        </div>
      </div>

      <div>
        <p
          class="mb-2 text-sm font-semibold tracking-widest text-indigo-600 uppercase dark:text-indigo-400"
        >
          About me
        </p>
        <h1 class="mb-5 text-4xl font-extrabold tracking-tight sm:text-5xl">
          Hello, I'm <span class="text-gradient">Morn Sreynich</span>
        </h1>
        <p class="mb-4 text-sm font-medium text-slate-500 dark:text-slate-400">
          쓰레이닟 · Nich09 · 📍 Cambodia
        </p>
        <p class="mb-4 text-lg leading-relaxed text-slate-600 dark:text-slate-300">
          I'm a software developer who builds and maintains scraping modules that pull data from
          banks and card companies in Japan, Vietnam, the UAE, India, and other countries.
        </p>
        <p class="text-lg leading-relaxed text-slate-600 dark:text-slate-300">
          I work with a Korean-speaking team, so my code and messages mix Korean, Japanese, and
          English. Next, I'm preparing to start an evening master's program in Data Science
          alongside my job.
        </p>
      </div>
    </div>

    <!-- Experience -->
    <div class="mt-20">
      <h2 class="mb-8 text-2xl font-bold sm:text-3xl">Experience</h2>
      <div
        class="rounded-2xl border border-slate-200 bg-white p-6 sm:p-8 dark:border-slate-800 dark:bg-slate-900"
      >
        <div class="mb-4 flex flex-wrap items-center justify-between gap-2">
          <h3 class="text-xl font-semibold">Software Developer</h3>
          <span
            class="rounded-full bg-emerald-50 px-3 py-0.5 text-xs font-semibold text-emerald-700 dark:bg-emerald-500/15 dark:text-emerald-300"
            >Current</span
          >
        </div>
        <ul class="mb-6 space-y-2 text-slate-600 dark:text-slate-300">
          <li class="flex gap-2">
            <span class="text-indigo-500">▹</span>Build and maintain scraping modules that collect
            data from banks and card companies.
          </li>
          <li class="flex gap-2">
            <span class="text-indigo-500">▹</span>Collaborate with a Korean-speaking team across
            Korean, Japanese, and English.
          </li>
        </ul>
        <div class="grid gap-6 sm:grid-cols-2">
          <div>
            <p class="mb-2 text-xs font-semibold tracking-widest text-slate-400 uppercase">
              Countries covered
            </p>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="c in countries"
                :key="c"
                class="rounded-full bg-indigo-50 px-3 py-1 text-sm text-indigo-700 dark:bg-indigo-500/15 dark:text-indigo-300"
                >{{ c }}</span
              >
            </div>
          </div>
          <div>
            <p class="mb-2 text-xs font-semibold tracking-widest text-slate-400 uppercase">
              Working languages
            </p>
            <div class="flex flex-wrap gap-2">
              <span
                v-for="l in languages"
                :key="l"
                class="rounded-full bg-fuchsia-50 px-3 py-1 text-sm text-fuchsia-700 dark:bg-fuchsia-500/15 dark:text-fuchsia-300"
                >{{ l }}</span
              >
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Skills -->
    <div class="mt-20">
      <h2 class="mb-2 text-2xl font-bold sm:text-3xl">Skills</h2>
      <p class="mb-8 text-slate-500 dark:text-slate-400">Technologies I work with.</p>
      <div class="grid grid-cols-1 gap-4 sm:grid-cols-2 lg:grid-cols-3">
        <SkillBadge
          v-for="skill in skills"
          :key="skill.name"
          :icon="skill.icon"
          :name="skill.name"
          :level="skill.level"
        />
      </div>
    </div>

    <!-- Education -->
    <div class="mt-20">
      <h2 class="mb-8 text-2xl font-bold sm:text-3xl">Education</h2>
      <div class="relative space-y-6 border-l-2 border-indigo-200 pl-8 dark:border-indigo-500/30">
        <div class="relative">
          <span
            class="absolute top-6 -left-[41px] h-4 w-4 rounded-full border-4 border-slate-50 bg-fuchsia-500 dark:border-slate-950"
          ></span>
          <div
            class="rounded-2xl border border-slate-200 bg-white p-6 dark:border-slate-800 dark:bg-slate-900"
          >
            <span
              class="mb-2 inline-block rounded-full bg-fuchsia-50 px-3 py-0.5 text-xs font-semibold text-fuchsia-600 dark:bg-fuchsia-500/15 dark:text-fuchsia-300"
              >Upcoming</span
            >
            <h3 class="text-lg font-semibold">Master's in Data Science</h3>
            <p class="text-slate-500 dark:text-slate-400">
              Evening program, alongside full-time work
            </p>
          </div>
        </div>
        <div class="relative">
          <span
            class="absolute top-6 -left-[41px] h-4 w-4 rounded-full border-4 border-slate-50 bg-indigo-500 dark:border-slate-950"
          ></span>
          <div
            class="rounded-2xl border border-slate-200 bg-white p-6 dark:border-slate-800 dark:bg-slate-900"
          >
            <span
              class="mb-2 inline-block rounded-full bg-indigo-50 px-3 py-0.5 text-xs font-semibold text-indigo-600 dark:bg-indigo-500/15 dark:text-indigo-300"
              >2026</span
            >
            <h3 class="text-lg font-semibold">Full-Stack Web Development Bootcamp</h3>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
