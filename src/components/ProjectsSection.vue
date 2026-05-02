<template>
  <section id="projects-section" class="py-5 bg-light">
    <div class="container py-4">
      <div class="text-center mb-5">
        <h2 class="section-title">My Projects</h2>
        <p class="text-muted mt-3">Real-world applications built with modern web technologies</p>
      </div>
      
      <div class="projects-container">
        <div class="row g-4">
          <div 
            v-for="project in projects" 
            :key="project.id || project.title"
            class="col-md-6 col-lg-4"
          >
            <ProjectCard :project="project" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from "vue";
import ProjectCard from "./ProjectCard.vue";

const projects = ref([]);
const isLoading = ref(true);

// Fetch projects from JSON file
onMounted(async () => {
  try {
    const response = await fetch('/data/projects.json');
    const data = await response.json();
    projects.value = data;
    isLoading.value = false;
  } catch (error) {
    console.error('Error loading projects:', error);
    isLoading.value = false;
    // Fallback data in case JSON fails to load
    projects.value = [
      {
        id: 1,
        title: "E-Commerce App",
        description: "MERN E-Commerce Platform. The platform features dynamic product catalog with filtering and sorting, real-time search, seamless cart updates, secure checkout, and a comprehensive admin dashboard with real-time analytics and user management capabilities.",
        image: "https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80",
        source: "https://karl-capstone3-vuejs.vercel.app/"
      }
    ];
  }
});
</script>

<style scoped>
#projects-section {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  position: relative;
}

.section-title {
  font-weight: 700;
  font-size: 2.2rem;
  letter-spacing: -0.01em;
  margin-bottom: 0.5rem;
  position: relative;
  display: inline-block;
  color: #0f2b3d;
}

.section-title:after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 4px;
  background: #2c7da0;
  border-radius: 4px;
}

/* Loading State */
.loading-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 4px solid #e2e8f0;
  border-top-color: #1e6091;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

/* Responsive Design */
@media (max-width: 768px) {
  .section-title {
    font-size: 1.9rem;
  }
}

/* Animation for cards */
.col-md-6 {
  animation: fadeInUp 0.6s ease backwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Stagger animation for cards */
.col-md-6:nth-child(1) { animation-delay: 0.05s; }
.col-md-6:nth-child(2) { animation-delay: 0.1s; }
.col-md-6:nth-child(3) { animation-delay: 0.15s; }
.col-md-6:nth-child(4) { animation-delay: 0.2s; }
.col-md-6:nth-child(5) { animation-delay: 0.25s; }
.col-md-6:nth-child(6) { animation-delay: 0.3s; }
</style>
