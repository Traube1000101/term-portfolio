<script setup lang="ts">
  import { RouterLink } from 'vue-router';
  defineProps<{
    to: string;
  }>();
</script>

<template>
  <RouterLink class="nav-element" :to>
    <div>
      <slot></slot>
    </div>
    <div class="pseudo-bold">
      <slot></slot>
    </div>
  </RouterLink>
</template>

<style>
  .nav-element .pseudo-bold {
    height: 0;
    visibility: hidden;
    overflow: hidden;
    user-select: none;
    pointer-events: none;
    font-weight: bolder;
  }

  .nav-element.router-link-exact-active div {
    font-weight: bolder;
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
