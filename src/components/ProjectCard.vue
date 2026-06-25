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
  background: white;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: transform 0.3s;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-icon {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 1rem;
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