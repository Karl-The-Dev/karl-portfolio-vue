<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  project: {
    type: Object,
    required: true
  }
});

// State for showing full description
const showFullDescription = ref(false);

// Computed property for truncated or full description
const displayDescription = computed(() => {
  const description = props.project.description;
  const maxLength = 120;
  if (!description) return '';
  if (showFullDescription.value) return description;
  if (description.length <= maxLength) return description;
  return description.substring(0, maxLength) + '...';
});

// Check if description needs truncation
const needsTruncation = computed(() => {
  return props.project.description && props.project.description.length > 120;
});

// Toggle description function
const toggleDescription = () => {
  showFullDescription.value = !showFullDescription.value;
};

function handleSubmit(url) {
  window.open(url, '_blank');
}

// Handle image loading errors
const handleImageError = (event) => {
  event.target.src = 'https://placehold.co/600x400/1e6091/ffffff?text=Project+Image';
};
</script>

<template>
  <div class="project-card-wrapper">
    <div class="card project-card h-100">
      <div class="card-image-wrapper">
        <img 
          :src="project.image" 
          class="card-img-top project-image" 
          :alt="project.title"
          @error="handleImageError"
        >
        <div class="card-overlay">
          <button 
            type="submit" 
            class="btn-overlay" 
            @click="handleSubmit(project.source)"
          >
            <i class="bi bi-box-arrow-up-right"></i>
          </button>
        </div>
      </div>
      <div class="card-body project-body">
        <h5 class="card-title project-title">{{ project.title }}</h5>
        <p class="card-text project-description">
          {{ displayDescription }}
        </p>
        <div class="description-actions" v-if="needsTruncation">
          <button class="btn-show-more" @click="toggleDescription" type="button">
            <i :class="showFullDescription ? 'bi bi-chevron-up' : 'bi bi-chevron-down'"></i>
            {{ showFullDescription ? 'Show Less' : 'Show More' }}
          </button>
        </div>
        <div class="card-footer-actions">
          <button 
            type="submit" 
            class="btn btn-project rounded-pill" 
            @click="handleSubmit(project.source)"
          >
            <i class="bi bi-eye me-2"></i>View My Project
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.project-card-wrapper {
  height: 100%;
  animation: fadeInUp 0.6s ease backwards;
}

.project-card {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.2, 0, 0, 1);
  box-shadow: 0 10px 30px -12px rgba(0, 0, 0, 0.08);
  border: none;
  height: 100%;
  display: flex;
  flex-direction: column;
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 25px 35px -16px rgba(0, 0, 0, 0.15);
}

/* Image Wrapper */
.card-image-wrapper {
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #1e6091, #0f2b3d);
  aspect-ratio: 16 / 9;
}

.project-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}

.project-card:hover .project-image {
  transform: scale(1.05);
}

/* Overlay Effect */
.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(15, 43, 61, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .card-overlay {
  opacity: 1;
}

.btn-overlay {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: white;
  border: none;
  color: #1e6091;
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  transform: translateY(20px);
}

.project-card:hover .btn-overlay {
  transform: translateY(0);
}

.btn-overlay:hover {
  background: #2c7da0;
  color: white;
  transform: scale(1.1);
}

/* Card Body */
.project-body {
  padding: 1.5rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  background: white;
}

.project-title {
  font-size: 1.35rem;
  font-weight: 700;
  color: #0f2b3d;
  margin-bottom: 0.75rem;
  line-height: 1.4;
  transition: color 0.3s ease;
}

.project-card:hover .project-title {
  color: #1e6091;
}

.project-description {
  color: #475569;
  line-height: 1.6;
  font-size: 0.9rem;
  margin-bottom: 0.75rem;
  flex: 1;
}

/* Show More / Show Less Button Styles */
.description-actions {
  margin-bottom: 1rem;
  text-align: left;
}

.btn-show-more {
  background: transparent;
  border: 1px solid #e2e8f0;
  border-radius: 20px;
  color: #2c7da0;
  font-size: 0.8rem;
  font-weight: 600;
  padding: 0.4rem 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-show-more:hover {
  background: #f1f5f9;
  color: #1e6091;
  border-color: #2c7da0;
  transform: translateX(2px);
}

.btn-show-more i {
  font-size: 0.8rem;
  transition: transform 0.3s ease;
}

/* Card Footer Actions */
.card-footer-actions {
  margin-top: auto;
}

/* Project Button */
.btn-project {
  background: transparent;
  border: 2px solid #1e6091;
  color: #1e6091;
  padding: 0.7rem 1.2rem;
  font-weight: 600;
  font-size: 0.9rem;
  transition: all 0.3s ease;
  width: 100%;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
}

.btn-project:hover {
  background: #1e6091;
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 5px 12px -5px rgba(30, 96, 145, 0.4);
}

.btn-project i {
  transition: transform 0.3s ease;
}

.btn-project:hover i {
  transform: translateX(3px);
}

/* Responsive Design */
@media (max-width: 768px) {
  .project-body {
    padding: 1.25rem;
  }
  
  .project-title {
    font-size: 1.2rem;
  }
  
  .project-description {
    font-size: 0.85rem;
  }
  
  .btn-project {
    padding: 0.6rem 1rem;
    font-size: 0.85rem;
  }
  
  .btn-show-more {
    font-size: 0.75rem;
    padding: 0.35rem 0.8rem;
  }
}

@media (max-width: 576px) {
  .project-card {
    border-radius: 16px;
  }
  
  .project-body {
    padding: 1rem;
  }
  
  .btn-overlay {
    width: 40px;
    height: 40px;
    font-size: 1.2rem;
  }
  
  .btn-show-more {
    font-size: 0.7rem;
    padding: 0.3rem 0.7rem;
  }
}

/* Animation */
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
</style>