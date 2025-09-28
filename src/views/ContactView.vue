<template>
  <div class="contact">
    <!-- Hero Section -->
    <section class="contact-hero">
      <div class="container">
        <h1>Contactez-nous</h1>
        <p class="hero-subtitle">Prêt à démarrer votre prochaine collaboration ?</p>
      </div>
    </section>

    <!-- Contact Content -->
    <section class="contact-content">
      <div class="container">
        <div class="contact-grid">
          <!-- Contact Info -->
          <div class="contact-info">
            <h2>Parlons de votre projet</h2>
            <p>
              Que vous soyez un influenceur à la recherche de collaborations éthiques
              ou une entreprise souhaitant toucher une audience authentique, nous sommes
              là pour vous accompagner.
            </p>

            <div class="contact-methods">
              <div class="contact-method">
                <div class="method-icon">📧</div>
                <div class="method-info">
                  <h4>Email</h4>
                  <p>contact@muslimvisibility.fr</p>
                </div>
              </div>
              <div class="contact-method">
                <div class="method-icon">📱</div>
                <div class="method-info">
                  <h4>Téléphone</h4>
                  <p>+33 1 23 45 67 89</p>
                </div>
              </div>
              <div class="contact-method">
                <div class="method-icon">💬</div>
                <div class="method-info">
                  <h4>WhatsApp</h4>
                  <p>Réponse rapide garantie</p>
                </div>
              </div>
            </div>

            <!-- WhatsApp Button -->
            <div class="whatsapp-section">
              <h3>Besoin d'une réponse rapide ?</h3>
              <a href="https://wa.me/+33123456789?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services"
                 class="whatsapp-btn"
                 target="_blank">
                <span class="whatsapp-icon">💬</span>
                Discuter sur WhatsApp
              </a>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="contact-form-wrapper">
            <div class="form-card">
              <h3>Envoyez-nous un message</h3>
              <form @submit.prevent="submitForm" class="contact-form">
                <div class="form-group">
                  <label for="name">Nom complet *</label>
                  <input
                    type="text"
                    id="name"
                    v-model="form.name"
                    required
                    placeholder="Votre nom complet"
                  >
                </div>

                <div class="form-group">
                  <label for="email">Email *</label>
                  <input
                    type="email"
                    id="email"
                    v-model="form.email"
                    required
                    placeholder="votre@email.com"
                  >
                </div>

                <div class="form-group">
                  <label for="type">Vous êtes *</label>
                  <select id="type" v-model="form.type" required>
                    <option value="">Sélectionnez votre profil</option>
                    <option value="influenceur">Influenceur</option>
                    <option value="entreprise">Entreprise</option>
                    <option value="autre">Autre</option>
                  </select>
                </div>

                <div class="form-group">
                  <label for="phone">Téléphone (optionnel)</label>
                  <input
                    type="tel"
                    id="phone"
                    v-model="form.phone"
                    placeholder="+33 1 23 45 67 89"
                  >
                </div>

                <div class="form-group">
                  <label for="message">Message *</label>
                  <textarea
                    id="message"
                    v-model="form.message"
                    required
                    rows="5"
                    placeholder="Décrivez votre projet, vos besoins ou vos questions..."
                  ></textarea>
                </div>

                <button
                  type="submit"
                  class="submit-btn"
                  :disabled="isSubmitting"
                >
                  <span v-if="!isSubmitting">Envoyer le message</span>
                  <span v-else>Envoi en cours...</span>
                </button>

                <div v-if="submitted" class="success-message">
                  ✅ Merci ! Votre message a été envoyé. Nous vous recontacterons rapidement.
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ Section -->
    <section class="faq-section">
      <div class="container">
        <h2>Questions fréquentes</h2>
        <div class="faq-grid">
          <div class="faq-item">
            <h4>Combien de temps pour avoir une réponse ?</h4>
            <p>Nous nous engageons à répondre sous 24h en semaine, et souvent bien plus rapidement via WhatsApp.</p>
          </div>
          <div class="faq-item">
            <h4>Quels sont vos tarifs ?</h4>
            <p>Nos tarifs varient selon le type de collaboration. Contactez-nous pour un devis personnalisé et transparent.</p>
          </div>
          <div class="faq-item">
            <h4>Travaillez-vous avec tous types d'influenceurs ?</h4>
            <p>Nous travaillons avec des créateurs de contenu alignés avec nos valeurs d'éthique et d'authenticité.</p>
          </div>
          <div class="faq-item">
            <h4>Comment garantissez-vous la qualité ?</h4>
            <p>Chaque collaboration est suivie personnellement par notre équipe pour assurer des résultats optimaux.</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  type: '',
  phone: '',
  message: ''
})

const isSubmitting = ref(false)
const submitted = ref(false)

const submitForm = async () => {
  isSubmitting.value = true

  // Simulation d'envoi de formulaire
  setTimeout(() => {
    isSubmitting.value = false
    submitted.value = true

    // Reset form after success
    setTimeout(() => {
      form.value = {
        name: '',
        email: '',
        type: '',
        phone: '',
        message: ''
      }
      submitted.value = false
    }, 3000)
  }, 1500)
}
</script>

<style scoped>
.contact {
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.contact-hero {
  background: linear-gradient(135deg, #2c5aa0 0%, #1e3f73 100%);
  color: white;
  padding: 6rem 0 4rem;
  text-align: center;
}

.contact-hero h1 {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.hero-subtitle {
  font-size: 1.3rem;
  opacity: 0.9;
}

.contact-content {
  padding: 5rem 0;
  background: #f8f9fa;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}

.contact-info h2 {
  font-size: 2.2rem;
  margin-bottom: 1.5rem;
  color: #333;
}

.contact-info > p {
  font-size: 1.1rem;
  color: #666;
  line-height: 1.6;
  margin-bottom: 2.5rem;
}

.contact-methods {
  margin-bottom: 3rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.method-icon {
  font-size: 2rem;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f0f7ff;
  border-radius: 50%;
}

.method-info h4 {
  margin-bottom: 0.3rem;
  color: #333;
}

.method-info p {
  color: #666;
  margin: 0;
}

.whatsapp-section {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  text-align: center;
}

.whatsapp-section h3 {
  margin-bottom: 1.5rem;
  color: #333;
}

.whatsapp-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: #25D366;
  color: white;
  padding: 1rem 2rem;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  font-size: 1.1rem;
}

.whatsapp-btn:hover {
  background: #20B954;
  transform: translateY(-2px);
}

.whatsapp-icon {
  font-size: 1.2rem;
}

.form-card {
  background: white;
  padding: 2.5rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.form-card h3 {
  font-size: 1.8rem;
  margin-bottom: 2rem;
  color: #333;
  text-align: center;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  font-weight: 600;
  color: #333;
}

.form-group input,
.form-group select,
.form-group textarea {
  padding: 1rem;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #2c5aa0;
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  background: #2c5aa0;
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.submit-btn:hover:not(:disabled) {
  background: #1e3f73;
  transform: translateY(-2px);
}

.submit-btn:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.success-message {
  background: #d4edda;
  color: #155724;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  font-weight: 500;
}

.faq-section {
  padding: 5rem 0;
  background: white;
}

.faq-section h2 {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  color: #333;
}

.faq-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.faq-item {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 15px;
  border-left: 4px solid #2c5aa0;
}

.faq-item h4 {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: #333;
}

.faq-item p {
  color: #666;
  line-height: 1.6;
  margin: 0;
}

@media (max-width: 768px) {
  .contact-hero h1 {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1.1rem;
  }

  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .container {
    padding: 0 1rem;
  }

  .form-card {
    padding: 1.5rem;
  }

  .contact-method {
    flex-direction: column;
    text-align: center;
  }

  .method-icon {
    margin-bottom: 0.5rem;
  }

  .faq-grid {
    grid-template-columns: 1fr;
  }
}
</style>