<template>
  <section id="projects">
    <div class="container">
      <span class="section-label">Portfolio</span>
      <h2 class="section-title">My <span>Projects</span></h2>

      <div class="row g-4 justify-content-center">
        <div
          v-for="project in projects"
          :key="project.id"
          class="col-lg-4 col-md-6"
        >
          <ProjectCard :project="project" />
        </div>
      </div>

    </div>
  </section>
</template>

<script setup>
import ProjectCard from './ProjectCard.vue'
import projects from '../data/projects.json'
</script>