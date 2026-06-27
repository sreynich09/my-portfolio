<template>
  <div class="project-card">
    <div class="project-icon">{{ project.emoji }}</div>
    <h3>{{ project.title }}</h3>
    <p>{{ project.description }}</p>
    <div class="tech-tags">
      <span v-for="tech in project.technologies" :key="tech" class="tag">
        {{ tech }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProjectCard',
  props: {
    project: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.project-card {
  background: var(--color-surface);
  color: var(--color-text);
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
}

.project-card h3 {
  color: var(--color-text);
}

.project-card p {
  color: var(--color-text-muted);
}

.project-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 12px 24px rgba(0,0,0,0.15);
}

.project-icon {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 1rem;
  transition: transform 0.3s ease;
}

.project-card:hover .project-icon {
  transform: scale(1.15) rotate(-5deg);
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 1rem;
}

.tag {
  padding: 0.25rem 0.75rem;
  background: #e0f2fe;
  color: #0369a1;
  border-radius: 12px;
  font-size: 0.875rem;
}
</style>