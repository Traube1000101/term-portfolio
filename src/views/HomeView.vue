<script setup lang="ts">
  import TerminalContainer from '../components/TerminalContainer.vue';
</script>

<template>
  <main>
    <TerminalContainer />
  </main>
</template>

<style scoped>
  main {
    width: 100%;
    height: 50vh;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
