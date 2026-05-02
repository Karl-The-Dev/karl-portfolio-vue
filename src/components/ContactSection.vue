<template>
  <section id="contact-section" class="py-5">
    <div class="container py-4">
      <div class="text-center mb-5">
        <h2 class="section-title">Let's Connect</h2>
        <p class="text-muted mt-3">Have a project in mind or just want to chat about tech? Reach out!</p>
      </div>
      
      <div class="row justify-content-center">
        <div class="col-lg-10">
          <div class="contact-card">
            <div class="row g-0">
              <!-- Map Section - Left Side -->
              <div class="col-md-6 p-4 p-md-5 map-section">
                <div class="map-wrapper">
                  <iframe 
                    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3860.395389963708!2d121.04668217599457!3d14.632485776137637!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397b7afde2bffff%3A0xfb6ed19aaf10bfe6!2sPhilippine%20Heart%20Center!5e0!3m2!1sen!2sph!4v1699984567890!5m2!1sen!2sph" 
                    width="100%" 
                    height="300" 
                    style="border:0; border-radius: 16px;" 
                    allowfullscreen="" 
                    loading="lazy" 
                    referrerpolicy="no-referrer-when-downgrade">
                  </iframe>
                </div>
                <div class="address-wrapper mt-4">
                  <i class="bi bi-geo-alt-fill location-icon"></i>
                  <p class="address-text mt-2">
                    Philippine Heart Center Bldg, East Avenue, cor Matalino St, Quezon City, Metro Manila
                  </p>
                </div>
              </div>
              
              <!-- Contact Form Section - Right Side -->
              <div class="col-md-6 p-4 p-md-5 form-section">
                <h3 class="form-title mb-4">
                  <i class="bi bi-envelope-paper me-2"></i>Send a Message
                </h3>
                
                <form @submit.prevent="submitForm">
                  <!-- Name Field -->
                  <div class="mb-4">
                    <label for="nameInput" class="form-label fw-semibold">
                      <i class="bi bi-person me-1"></i>Full Name
                    </label>
                    <input 
                      type="text" 
                      class="form-control form-control-lg" 
                      id="nameInput" 
                      placeholder="John M. Doe"
                      v-model="name"
                      :disabled="isLoading"
                      required
                    >
                  </div>
                  
                  <!-- Email Field -->
                  <div class="mb-4">
                    <label for="emailInput" class="form-label fw-semibold">
                      <i class="bi bi-envelope me-1"></i>Email Address
                    </label>
                    <input 
                      type="email" 
                      class="form-control form-control-lg" 
                      id="emailInput" 
                      placeholder="john@example.com"
                      v-model="email"
                      :disabled="isLoading"
                      required
                    >
                  </div>
                  
                  <!-- Message Field -->
                  <div class="mb-4">
                    <label for="messageTextarea" class="form-label fw-semibold">
                      <i class="bi bi-chat-text me-1"></i>Message
                    </label>
                    <textarea 
                      class="form-control" 
                      id="messageTextarea" 
                      rows="4" 
                      placeholder="Tell me about your project or opportunity..."
                      v-model="message"
                      :disabled="isLoading"
                      required
                    ></textarea>
                  </div>
                  
                  <!-- Social Links and reCAPTCHA Row -->
                  <div class="row align-items-center mt-3">
                    <div class="col-md-12 mb-3">
                      <div class="d-flex justify-content-start gap-3 social-links">
                        <a href="https://www.linkedin.com/in/kharlo-ramos-7bb528374/" 
                           class="social-icon-link" 
                           target="_blank" 
                           aria-label="LinkedIn">
                          <i class="bi bi-linkedin"></i>
                        </a>
                        <a href="https://github.com/Karl-The-Dev" 
                           class="social-icon-link" 
                           target="_blank" 
                           aria-label="GitHub">
                          <i class="bi bi-github"></i>
                        </a>
                        <!-- <a href="#" 
                           class="social-icon-link" 
                           target="_blank" 
                           aria-label="Twitter">
                          <i class="bi bi-twitter-x"></i>
                        </a>
                        <a href="#" 
                           class="social-icon-link" 
                           target="_blank" 
                           aria-label="Stack Overflow">
                          <i class="bi bi-stack-overflow"></i>
                        </a> -->
                      </div>
                    </div>
                  </div>
                  
                  <!-- reCAPTCHA Container - FIXED VISIBILITY -->
                  <div class="d-flex justify-content-start mt-3 mb-3">
                    <div ref="recaptchaContainer" class="recaptcha-wrapper"></div>
                  </div>
                  
                  <!-- Submit Button -->
                  <div class="row mt-2">
                    <div class="col-12">
                      <button 
                        type="submit" 
                        class="btn btn-custom btn-lg w-100"
                        :disabled="isLoading"
                      >
                        <i v-if="!isLoading" class="bi bi-send-check me-2"></i>
                        <i v-else class="bi bi-hourglass-split me-2"></i>
                        {{ isLoading ? 'Sending...' : 'Send Message' }}
                      </button>
                    </div>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import { Notyf } from "notyf";
import "notyf/notyf.min.css";

const notyf = new Notyf({
  duration: 3000,
  position: { x: 'right', y: 'top' },
  types: [
    {
      type: 'success',
      background: '#1e6091',
      icon: { className: 'bi bi-check-circle', tagName: 'i' }
    },
    {
      type: 'error',
      background: '#dc3545',
      icon: { className: 'bi bi-exclamation-circle', tagName: 'i' }
    }
  ]
});

const WEB3FORMS_ACCESS_KEY = "70c7f30a-ca7d-44f4-bd48-422768b724b2";

// Email subject
const subject = "New message from Developer Portfolio Contact Form";

// Form data
const name = ref("");
const email = ref("");
const message = ref("");
const isLoading = ref(false);

// Submit form
const submitForm = async () => {
  // Check if reCAPTCHA token is present
  if (!recaptchaToken.value) {
    notyf.error("Please verify that you are not a robot");
    return;
  }

  // Validate form fields
  if (!name.value.trim() || !email.value.trim() || !message.value.trim()) {
    notyf.error("Please fill in all fields");
    return;
  }

  // Validate email format
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email.value)) {
    notyf.error("Please enter a valid email address");
    return;
  }

  isLoading.value = true;

  try {
    const response = await fetch("https://api.web3forms.com/submit", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Accept": "application/json"
      },
      body: JSON.stringify({
        access_key: WEB3FORMS_ACCESS_KEY,
        subject: subject,
        name: name.value,
        email: email.value,
        message: message.value
      })
    });

    const result = await response.json();

    if (result.success) {
      console.log(result);
      isLoading.value = false;
      notyf.success("Message sent successfully!");
      
      // Reset form
      name.value = "";
      email.value = "";
      message.value = "";
      
      // Reset reCAPTCHA
      resetRecaptcha();
    } else {
      isLoading.value = false;
      notyf.error("Failed to send message. Please try again.");
    }
  } catch (error) {
    console.error(error);
    isLoading.value = false;
    notyf.error("Network error. Please check your connection.");
  }
};


const SITE_KEY = "6LdTj38sAAAAAEng_olZ646hMIHxVbt49d9gHkc8";

const recaptchaContainer = ref(null);
const recaptchaWidgetId = ref(null);
const recaptchaToken = ref('');

// Callback called by reCAPTCHA when successful
function onRecaptchaSuccess(token) {
  recaptchaToken.value = token;
  console.log("reCAPTCHA verified successfully");
}

// Callback when expired
function onRecaptchaExpired() {
  recaptchaToken.value = '';
  notyf.warning("reCAPTCHA expired. Please verify again.");
}

// Function to render the reCAPTCHA widget
function renderRecaptcha() {
  if (!window.grecaptcha) {
    console.error('reCAPTCHA not loaded');
    return;
  }

  // Check if container exists and widget isn't already rendered
  if (recaptchaContainer.value && recaptchaWidgetId.value === null) {
    try {
      recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
        sitekey: SITE_KEY,
        size: 'normal',
        callback: onRecaptchaSuccess,
        'expired-callback': onRecaptchaExpired,
      });
      console.log("reCAPTCHA rendered successfully");
    } catch (error) {
      console.error("Error rendering reCAPTCHA:", error);
    }
  }
}

// Function to reset reCAPTCHA
function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null && window.grecaptcha) {
    try {
      window.grecaptcha.reset(recaptchaWidgetId.value);
      recaptchaToken.value = '';
      console.log("reCAPTCHA reset");
    } catch (error) {
      console.error("Error resetting reCAPTCHA:", error);
    }
  }
}

// Load reCAPTCHA on mount
onMounted(() => {
  // Check if reCAPTCHA script is already loaded
  if (window.grecaptcha && window.grecaptcha.render) {
    renderRecaptcha();
  } else {
    // Wait for reCAPTCHA to load
    const checkInterval = setInterval(() => {
      if (window.grecaptcha && window.grecaptcha.render) {
        clearInterval(checkInterval);
        renderRecaptcha();
      }
    }, 100);
    
    onBeforeUnmount(() => {
      clearInterval(checkInterval);
    });
  }
});
</script>

<style scoped>
/* Contact Section Styling */
#contact-section {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  position: relative;
}

.contact-card {
  background: white;
  border-radius: 2rem;
  overflow: hidden;
  box-shadow: var(--card-shadow);
  transition: 0.3s ease;
}

.contact-card:hover {
  box-shadow: 0 30px 40px -20px rgba(0, 0, 0, 0.15);
}

/* Map Section */
.map-section {
  background: linear-gradient(145deg, #f8fafc, #ffffff);
  border-right: 1px solid rgba(0, 0, 0, 0.05);
}

.map-wrapper {
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
}

.address-wrapper {
  text-align: center;
}

.location-icon {
  font-size: 2rem;
  color: #2c7da0;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.address-text {
  color: #475569;
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 0;
}

/* Form Section */
.form-section {
  background: white;
}

.form-title {
  font-weight: 700;
  color: #0f2b3d;
  font-size: 1.8rem;
  border-left: 4px solid #2c7da0;
  padding-left: 1rem;
}

.form-label {
  color: #1e293b;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.form-control {
  border: 2px solid #e2e8f0;
  border-radius: 12px;
  padding: 0.75rem 1rem;
  transition: all 0.2s ease;
  font-size: 1rem;
}

.form-control:focus {
  border-color: #2c7da0;
  box-shadow: 0 0 0 3px rgba(44, 125, 160, 0.1);
  outline: none;
}

.form-control:disabled {
  background-color: #f8fafc;
  opacity: 0.7;
}

/* Social Icons */
.social-links {
  margin-bottom: 0.5rem;
}

.social-icon-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  background: #f1f5f9;
  border-radius: 50%;
  font-size: 1.5rem;
  color: #1e6091;
  transition: all 0.3s ease;
  text-decoration: none;
}

.social-icon-link:hover {
  background: #1e6091;
  color: white;
  transform: translateY(-3px);
  box-shadow: 0 8px 15px -6px rgba(30, 96, 145, 0.3);
}

/* reCAPTCHA Container Styles - FIXED VISIBILITY */
.recaptcha-wrapper {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  min-height: 78px;
  background: transparent;
  border-radius: 8px;
}

/* Ensure reCAPTCHA iframe is visible */
:deep(.g-recaptcha) {
  margin: 0;
  transform: scale(0.98);
  transform-origin: left center;
}

/* Custom Button */
.btn-custom {
  background: #1e6091;
  border: none;
  padding: 0.875rem 1.8rem;
  font-weight: 600;
  border-radius: 40px;
  transition: all 0.25s ease;
  color: white;
  font-size: 1rem;
}

.btn-custom:hover:not(:disabled) {
  background: #0f2b3d;
  transform: translateY(-2px);
  box-shadow: 0 8px 20px -8px rgba(0, 0, 0, 0.3);
}

.btn-custom:disabled {
  opacity: 0.7;
  cursor: not-allowed;
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

/* Responsive Design */
@media (max-width: 768px) {
  .map-section {
    border-right: none;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
  }
  
  .map-wrapper iframe {
    height: 250px;
  }
  
  .form-title {
    font-size: 1.5rem;
  }
  
  .section-title {
    font-size: 1.9rem;
  }
  
  .btn-custom {
    width: 100%;
  }
  
  .social-icon-link {
    width: 42px;
    height: 42px;
    font-size: 1.25rem;
  }
  
  /* Adjust reCAPTCHA for mobile */
  .recaptcha-wrapper {
    justify-content: center;
  }
  
  :deep(.g-recaptcha) {
    transform: scale(0.85);
  }
}

@media (max-width: 576px) {
  .contact-card {
    border-radius: 1.5rem;
  }
  
  .map-section,
  .form-section {
    padding: 1.5rem !important;
  }
  
  .map-wrapper iframe {
    height: 200px;
  }
  
  /* Further adjust reCAPTCHA for small screens */
  :deep(.g-recaptcha) {
    transform: scale(0.77);
  }
}

/* Notyf custom positioning */
:deep(.notyf) {
  font-family: 'Inter', system-ui, sans-serif;
  border-radius: 12px;
}

:deep(.notyf__toast) {
  border-radius: 12px;
  padding: 12px 20px;
}

/* Loading spinner animation */
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.bi-hourglass-split {
  animation: spin 1s linear infinite;
  display: inline-block;
}
</style>
