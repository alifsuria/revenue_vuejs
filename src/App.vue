<script setup>
import { RouterLink, RouterView } from 'vue-router'
// import HelloWorld from './components/HelloWorld.vue'r
</script>

<template>
  <!-- <div> -->
  <!-- <ul class="nav nav-pills">
    <li class="nav-item">
      <RouterLink class="nav-link active" to="/">Create New</RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink class="nav-link" :to="{name:'group_item'}">Revenue Group Item</RouterLink>
    </li>
  </ul> -->
  <!-- </div> -->

  <RouterView />
</template>

<style scoped></style>
