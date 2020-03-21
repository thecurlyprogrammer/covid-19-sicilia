<template>
  <div id="app">
    <navbar />
    <router-view/>
    <bottom />
  </div>
</template>

<script>
import navbar from '@/components/navbar.vue';
import bottom from '@/components/footer.vue';

export default {
  components: {
    navbar,
    bottom,
  },
};
</script>

<style>
  html{
    height: 100%;
    scroll-behavior: smooth;
    -webkit-overflow-scrolling: touch;
  }
  body{
    height: 100%;
    background-color: #f5f6fa;
  }
</style>
