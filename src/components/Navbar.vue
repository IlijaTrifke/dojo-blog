<template>
  <header>
    <h1>The Dojo Blog</h1>
    <nav>
      <RouterLink :to="{ name: 'home' }">Home</RouterLink>
      <RouterLink :to="{ name: 'create' }">Create Post</RouterLink>
    </nav>
  </header>
</template>

<script>
export default {};
</script>

<style>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px;
}
header h1 {
  color: #444;
  font-size: 48px;
}
header a {
  color: #7e7676;
  text-decoration: none;
  margin-left: 20px;
}
header a.router-link-active {
  color: #444;
  font-weight: bold;
}
</style>
