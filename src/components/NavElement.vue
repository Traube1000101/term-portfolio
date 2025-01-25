<script setup lang="ts">
  import { RouterLink } from 'vue-router';
  defineProps<{
    to: string;
  }>();
</script>

<template>
  <RouterLink class="nav-element" :to>
    <slot></slot>
  </RouterLink>
</template>

<style>
  .nav-element.router-link-exact-active {
    -webkit-text-stroke: 0.05em var(--color-raspberry);
  }

  .nav-element.router-link-exact-active:hover {
    background-color: transparent;
  }

  .nav-element {
    display: inline-block;
    padding: 0 2rem;
    border-left: 1px solid var(--color-border);
  }

  .nav-element:first-of-type {
    border: 0;
  }
</style>
