<script setup>
import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
   <div class="wrapper">
      <nav class="d-flex justify-content-evenly">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <!-- <RouterLink to="/toggle">Toggle</RouterLink> -->
      </nav>
       <RouterView />
    </div>
</template>

<style lang="scss" scoped>

</style>