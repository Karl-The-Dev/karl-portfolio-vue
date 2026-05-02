<template>
  <section id="home" class="hero-section">
    <div class="container">
      <div class="row align-items-center gy-5">
        <div class="col-lg-7">
          <span class="hero-badge">
            <i class="bi bi-code-slash me-1"></i> Full-Stack Developer
          </span>
          <h1 class="display-name mt-2">Kharlo Ramos <br> Crafting Digital Solutions</h1>
          <p class="lead-text mt-3">I build scalable backend systems, elegant databases, and responsive frontends. Deep expertise in MERN, NoSQL, NodeJS, and semantic web technologies.</p>
          <div class="d-flex flex-wrap gap-3 mt-4">
            <a href="#projects-section" class="btn btn-custom border border-primary rounded-pill">
              <i class="bi bi-folder2-open me-1"></i> View Projects
            </a>
            <a href="#contact-section" class="btn btn-outline-custom border border-primary rounded-pill">
              <i class="bi bi-chat-dots me-1"></i> Let's Connect
            </a>
          </div>
        </div>
        <div class="col-lg-5 text-center">
          <div class="bg-white rounded-4 p-4 shadow-sm d-inline-block">
            <i class="bi bi-braces" style="font-size: 5rem; color: #2c7da0;"></i>
            <i class="bi bi-database" style="font-size: 4rem; color: #1e6091; margin-left: 0.5rem;"></i>
            <i class="bi bi-git" style="font-size: 4rem; color: #0f2b3d; margin-left: 0.5rem;"></i>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// Hero section component - no additional logic needed
</script>

<style scoped>
.hero-section {
  padding: 5rem 0 4rem 0;
  background: linear-gradient(145deg, #ffffff 0%, #f1f5f9 100%);
  border-bottom: 1px solid rgba(0,0,0,0.05);
}

.hero-badge {
  background: #e2e8f0;
  color: #0f172a;
  font-size: 0.85rem;
  font-weight: 600;
  padding: 0.35rem 1rem;
  border-radius: 40px;
  display: inline-block;
  margin-bottom: 1.2rem;
}

.display-name {
  font-weight: 800;
  font-size: 3.2rem;
  letter-spacing: -0.02em;
  background: linear-gradient(to right, #0f2b3d, #2c7da0);
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
}

.lead-text {
  font-size: 1.2rem;
  color: #334155;
  max-width: 90%;
  border-left: 4px solid #2c7da0;
  padding-left: 1rem;
}

@media (max-width: 768px) {
  .display-name {
    font-size: 2.3rem;
  }
  .lead-text {
    max-width: 100%;
  }
  .hero-section {
    padding: 3rem 0 2.5rem;
  }
}
</style>
