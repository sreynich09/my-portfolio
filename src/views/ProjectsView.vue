<template>
  <section class="mx-auto max-w-6xl px-4 py-16 sm:px-6 sm:py-24">
    <div class="mb-14 text-center">
      <p
        class="mb-2 text-sm font-semibold tracking-widest text-indigo-600 uppercase dark:text-indigo-400"
      >
        Portfolio
      </p>
      <h1 class="mb-4 text-4xl font-extrabold tracking-tight sm:text-5xl">
        My <span class="text-gradient">Projects</span>
      </h1>
      <p class="mx-auto max-w-xl text-lg text-slate-500 dark:text-slate-400">
        Here are some projects I've built
      </p>
    </div>

    <div class="mx-auto grid max-w-4xl gap-6 sm:grid-cols-2">
      <ProjectCard v-for="project in projects" :key="project.id" :project="project" />
    </div>
  </section>
</template>

<script>
import ProjectCard from '@/components/ProjectCard.vue'

export default {
  name: 'ProjectsView',
  components: {
    ProjectCard,
  },
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'User Directory App',
          emoji: '👥',
          image: `${import.meta.env.BASE_URL}images/user-directory.png`,
          description:
            'Browse and manage user profiles with search, filters, dynamic profile pages, profile editing, and shareable filtered URLs.',
          technologies: ['Vue 3', 'Vue Router 4', 'Vite', 'Tailwind CSS'],
          github: 'https://github.com/sreynich09/user-directory-app',
        },
        {
          id: 2,
          title: 'Blog API Authorization',
          emoji: '🔐',
          description:
            'A REST API for a blog with JWT authentication, role-based access (user, editor, admin), owner-or-admin rules for posts and comments, and admin-only user management.',
          technologies: ['Node.js', 'Express', 'MongoDB', 'Mongoose', 'JWT', 'bcryptjs'],
          github: 'https://github.com/sreynich09/authorization-routes',
        },
      ],
    }
  },
}
</script>
