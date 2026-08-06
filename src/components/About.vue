<template>
  <!-- ===================== HERO / ABOUT ===================== -->
  <section id="landing">
    <div class="hero-ring"></div>
    <div class="container position-relative" style="z-index:1;">
      <div class="row align-items-center gy-5">

        <!-- Photo -->
        <div class="col-lg-4 text-center">
          <div class="hero-photo-wrap mx-auto">
            <div class="hero-photo-inner">
              <!-- Replace with your actual photo filename -->
              <img src="/images/tamtechpic.png" alt="Profile Photo"
                onerror="this.parentElement.innerHTML='<div class=\'hero-photo-fallback\'>📷<br>Add your photo here</div>'" />
            </div>
          </div>
        </div>

        <!-- Text -->
        <div class="col-lg-8">
          <span class="hero-role">Full Stack Web Developer</span>
          <h1 class="hero-name">Hi, I'm <span class="accent">Jareth Ronquillo</span></h1>
          <p class="hero-desc">
            Hi, I'm Jareth Ronquillo, a Full Stack Web Developer from Oriental Mindoro, Philippines. I develop
            responsive and user-focused web applications using modern technologies, with a strong interest in backend
            development, clean architecture, and continuous learning.
          </p>
          <div class="d-flex flex-wrap gap-3">
            <a href="#projects" class="btn-primary-custom">View My Work</a>
            <!-- <a href="#contact" class="btn-outline-custom">Contact Me</a> -->
            <a href="https://drive.google.com/file/d/1KciaZTEroFUleXJIYY0mbaxrf5_66OqY/view" class="btn-resume-custom"
              target="_blank">View My Resume</a>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>