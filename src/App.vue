<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg sticky-top">
      <div class="container">
        <a class="navbar-brand" href="#">&lt;Karl Dev /&gt;</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarMain" aria-controls="navbarMain" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarMain">
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0 gap-2">
            <li class="nav-item"><a class="nav-link" href="#home">Home</a></li>
            <li class="nav-item"><a class="nav-link" href="#skills-section">Skills</a></li>
            <li class="nav-item"><a class="nav-link" href="#projects-section">Projects</a></li>
            <li class="nav-item"><a class="nav-link" href="#contact-section">Contact</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <HeroSection />
    <SkillsSection />
    <ProjectsSection />
    <ContactSection />
    <AppFooter />
  </div>
</template>

<script setup>
import HeroSection from './components/HeroSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import AppFooter from './components/AppFooter.vue'
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  background: #f8fafc;
  color: #0f172a;
  scroll-behavior: smooth;
}

:root {
  --primary-deep: #0f2b3d;
  --accent-teal: #2c7da0;
  --accent-blue: #1e6091;
  --soft-gray: #e9ecef;
  --card-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0,0,0,0.02);
}

.navbar {
  background: rgba(255, 255, 255, 0.96);
  backdrop-filter: blur(4px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.03);
  padding: 1rem 0;
}

.navbar-brand {
  font-weight: 800;
  font-size: 1.7rem;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #1e6091, #2c7da0);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

.nav-link {
  font-weight: 500;
  color: #1e293b;
  margin: 0 0.25rem;
  transition: 0.2s;
}

.nav-link:hover {
  color: #2c7da0;
  transform: translateY(-1px);
}

.btn-custom {
  background: #1e6091;
  border: none;
  padding: 0.7rem 1.8rem;
  font-weight: 600;
  border-radius: 40px;
  transition: 0.25s;
  color: white;
}

.btn-custom:hover {
  background: #0f2b3d;
  transform: translateY(-3px);
  box-shadow: 0 12px 18px -8px rgba(0,0,0,0.2);
}

.btn-outline-custom {
  border: 2px solid #1e6091;
  background: transparent;
  color: #1e6091;
  padding: 0.65rem 1.8rem;
  font-weight: 600;
  border-radius: 40px;
  transition: 0.2s;
}

.btn-outline-custom:hover {
  background: #1e6091;
  color: white;
  transform: translateY(-2px);
}

.section-title {
  font-weight: 700;
  font-size: 2.2rem;
  letter-spacing: -0.01em;
  margin-bottom: 0.5rem;
  position: relative;
  display: inline-block;
}

.section-title:after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 0;
  width: 60px;
  height: 4px;
  background: #2c7da0;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 1.9rem;
  }
}
</style>
