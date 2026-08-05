<template>
  <!-- Project X -->
        
    <div class="project-card">
      <div class="project-thumb">
        <img :src="project.image" alt="E-commerce App">
      </div>
      <div class="project-body">
        <span class="project-tag">E-Commerce</span>
        <h5>{{ project.title }}</h5>
        <p>{{ project.description }}</p>
        <div>
          <a :href="project.liveDemo" class="project-link" target="_blank" rel="nonopener nonreferrer">Live Demo</a>
          <a :href="project.github" class="project-link" target="_blank" >GitHub</a>
        </div>
      </div>
    </div>
        
</template>

<script setup>
  import { defineProps } from 'vue';

  defineProps({
    project: Object,
    required: true
  });

</script>