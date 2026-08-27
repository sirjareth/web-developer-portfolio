<template>
  <!-- ===================== NAVBAR ===================== -->
  <nav class="navbar navbar-expand-lg fixed-top" id="mainNav">
    <div class="container">
      <a class="navbar-brand" href="#landing">Port<span>folio</span></a>

      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navMenu"
        aria-controls="navMenu"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse justify-content-end" id="navMenu">
        <ul class="navbar-nav">
          <li class="nav-item"><a class="nav-link active" href="#landing">Home</a></li>
          <li class="nav-item"><a class="nav-link" href="#projects">My Projects</a></li>
          <li class="nav-item"><a class="nav-link" href="#tools">Tools</a></li>
          <li class="nav-item"><a class="nav-link" href="#contact">Contact</a></li>
        </ul>
        <!-- Resume Button -->
          <li class="nav-item ms-lg-3 d-flex align-items-center">
            <a href="https://drive.google.com/file/d/1LWolqkUS4szZUv07rKsTb7TlLSGbT-NK/view" target="_blank" class="resume-btn">
              Resume
            </a>
          </li>
      </div>
    </div>
  </nav>
</template>

<script setup>
  import { onMounted, onUnmounted } from 'vue'

  const handleScroll = () => {
    const sections = document.querySelectorAll('section[id]')
    const navLinks = document.querySelectorAll('.nav-link')

    let current = ''
    sections.forEach(sec => {
      if (window.scrollY >= sec.offsetTop - 100) {
        current = sec.getAttribute('id')
      }
    })

    navLinks.forEach(link => {
      link.classList.remove('active')
      if (link.getAttribute('href') === '#' + current) {
        link.classList.add('active')
      }
    })
  }

  onMounted(() => {
    window.addEventListener('scroll', handleScroll)
  })

  onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
  })
</script>