<template>
  <div class="projects-page">
    <h1>My Projects</h1>
    <p class="subtitle">Here are some projects I've built</p>
    
    <div class="projects-grid">
      <ProjectCard 
        v-for="project in projects" 
        :key="project.id"
        :project="project" />
    </div>
  </div>
</template>

<script>
import ProjectCard from '@/components/ProjectCard.vue'

export default {
  name: 'ProjectsView',
  components: {
    ProjectCard
  },
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Todo App',
          emoji: '✅',
          description: 'A task management app with localStorage persistence',
          technologies: ['Vue.js', 'Tailwind CSS', 'localStorage']
        },
        {
          id: 2,
          title: 'Movie Review App',
          emoji: '🎬',
          description: 'Rate and review your favorite movies',
          technologies: ['Vue.js', 'Components', 'Props & Events']
        },
        {
          id: 3,
          title: 'Recipe Manager',
          emoji: '🍳',
          description: 'Manage and organize your favorite recipes',
          technologies: ['Vue.js', 'Lifecycle Hooks', 'Computed Properties']
        }
      ]
    }
  }
}
</script>

<style scoped>
.projects-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 3rem 2rem;
}

h1 {
  text-align: center;
  color: var(--color-text);
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
}

.subtitle {
  text-align: center;
  color: var(--color-text-muted);
  font-size: 1.25rem;
  margin-bottom: 3rem;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}
</style>