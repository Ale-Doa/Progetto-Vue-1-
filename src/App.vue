<template>
  <div class="app">
    <nav>
      <RouterLink to="/" class="link">Home</RouterLink> |
      <RouterLink to="/about" class="link">About</RouterLink>
    </nav> 
    <RouterView />
  </div>
</template>

<style>
  .app {
    text-align: center;
  }
</style>