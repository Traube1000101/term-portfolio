<script setup lang="ts">
  import { RouterView } from 'vue-router';
  import Title from './components/PageTitle.vue';
  import NavElement from './components/NavElement.vue';
</script>

<template>
  <header>
    <div class="wrapper">
      <Title />
      <nav>
        <NavElement to="/">Home</NavElement>
        <NavElement to="/test">Another Page</NavElement>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
  header {
    line-height: 1.5;
    max-height: 100vh;
  }

  nav {
    width: 100%;
    font-size: 1.2rem;
    text-align: center;
    margin-top: 2rem;
  }
</style>
