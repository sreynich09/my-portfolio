<template>
  <div class="not-found">
    <div class="error-content">
      <h1>404</h1>
      <h2>Page Not Found</h2>
      <p>The page you're looking for doesn't exist.</p>
      <router-link to="/" class="home-button">
        Go Home
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NotFoundView'
}
</script>

<style scoped>
.not-found {
  min-height: 60vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.error-content h1 {
  font-size: 8rem;
  color: #42b983;
  margin: 0;
}

.error-content h2 {
  font-size: 2rem;
  color: var(--color-text);
  margin: 1rem 0;
}

.error-content p {
  color: var(--color-text-muted);
  margin-bottom: 2rem;
}

.home-button {
  display: inline-block;
  padding: 1rem 2rem;
  background: #42b983;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-weight: 600;
}

.home-button:hover {
  background: #369970;
}
</style>