<template>
  <section id="skills-section" class="py-5">
    <div class="container py-4">
      <div class="text-center mb-5">
        <h2 class="section-title">Technical Arsenal</h2>
        <p class="text-muted mt-3">Modern full-stack toolkit | version control | algorithms & database mastery</p>
      </div>
      <div class="skills-grid">
        <span v-for="skill in skills" :key="skill.name" class="skill-tag">
          <i :class="skill.icon"></i> {{ skill.name }}
        </span>
      </div>
      <div class="text-center mt-5">
        <div class="badge bg-light text-dark p-3 rounded-pill shadow-sm">
          <i class="bi bi-check-circle-fill text-success me-1"></i> 30+ core technologies & best practices
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  { name: 'HTML5', icon: 'bi bi-filetype-html' },
  { name: 'HTML Tags', icon: 'bi bi-code-slash' },
  { name: 'Semantic HTML', icon: 'bi bi-layout-text-window' },
  { name: 'Git', icon: 'bi bi-git' },
  { name: 'GitHub', icon: 'bi bi-github' },
  { name: 'GitLab', icon: 'bi bi-gitlab' },
  { name: 'Express JS', icon: 'bi bi-node-plus' },
  { name: 'MongoDB', icon: 'bi bi-database' },
  { name: 'API', icon: 'bi bi-plug' },
  { name: 'NoSQL', icon: 'bi bi-diagram-3' },
  { name: 'NodeJS', icon: 'bi bi-nodejs' },
  { name: 'Database Design', icon: 'bi bi-bezier2' },
  { name: 'NPM', icon: 'bi bi-box-seam' },
  { name: 'Database Management', icon: 'bi bi-server' },
  { name: 'Mongoose', icon: 'bi bi-mongodb' },
  { name: 'Algorithms', icon: 'bi bi-graph-up' },
  { name: 'Data Structures', icon: 'bi bi-bricks' },
  { name: 'Function Coding', icon: 'bi bi-braces-asterisk' },
  { name: 'CSS3', icon: 'bi bi-filetype-css' },
  { name: 'CSS', icon: 'bi bi-filetype-css' },
  { name: 'Bootstrap 5', icon: 'bi bi-bootstrap-fill' },
  { name: 'Bootstrap', icon: 'bi bi-bootstrap' },
  { name: 'App Building', icon: 'bi bi-phone-flip' }
]
</script>

<style scoped>
.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  justify-content: center;
}

.skill-tag {
  background: white;
  border-radius: 60px;
  padding: 0.6rem 1.3rem;
  font-weight: 500;
  font-size: 0.9rem;
  color: #0f2b3d;
  box-shadow: 0 2px 6px rgba(0,0,0,0.02), 0 1px 2px rgba(0,0,0,0.05);
  transition: all 0.2s ease;
  border: 1px solid #e2e8f0;
  display: inline-flex;
  align-items: center;
  gap: 8px;
}

.skill-tag i {
  font-size: 1.1rem;
  color: #2c7da0;
}

.skill-tag:hover {
  transform: translateY(-3px);
  border-color: #b9d8f0;
  box-shadow: 0 10px 15px -8px rgba(0,0,0,0.08);
  background: #ffffff;
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
