<script setup>
  import Sidebar from './components/Sidebar.vue';
</script>

<template>
  <div class="app">
    <!-- SIDEBAR -->
    <Sidebar />
    <router-view />
  </div>
</template>

<style lang="scss" scoped>


.app {
  display: flex;

  main {
    flex: 1 1 0;
    padding: 2rem;

    @media (max-width: 768px) {
      padding-left: 6rem;
    }
  }
}
</style>
