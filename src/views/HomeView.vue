<script setup lang="ts">
import { ref, onMounted } from 'vue'

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

// Animation on scroll with staggered delay
onMounted(() => {
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        // Ajouter un délai progressif pour les éléments dans le même conteneur
        const siblings = entry.target.parentElement?.querySelectorAll('.animate-on-scroll')
        const index = Array.from(siblings || []).indexOf(entry.target)

        setTimeout(() => {
          entry.target.classList.add('animate-in')
        }, index * 100)
      }
    })
  }, observerOptions)

  // Observer tous les éléments avec la classe 'animate-on-scroll'
  document.querySelectorAll('.animate-on-scroll').forEach(el => {
    observer.observe(el)
  })
})
</script>

<template>
  <div class="home">
    <!-- Hero Section -->
    <section id="accueil" class="hero">
      <div class="hero-background"></div>
      <div class="hero-content">
        <h1 class="hero-title animate-on-scroll">Muslim Visibility</h1>
        <p class="hero-slogan animate-on-scroll">Votre succès, notre engagement éthique</p>
        <p class="hero-description animate-on-scroll">
          Nous connectons les marques aux influenceurs musulmans avec transparence,
          respect et authenticité pour des campagnes qui font la différence.
        </p>
        <div class="hero-actions animate-on-scroll">
          <a href="https://wa.me/+33123456789?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services" class="btn btn-primary" target="_blank">
            💬 Nous contacter sur WhatsApp
          </a>
          <a href="#contact" class="btn btn-secondary">
            Demander un devis
          </a>
        </div>
      </div>
      <div class="hero-particles"></div>
    </section>

    <!-- About Section -->
    <section id="about" class="about-section">
      <div class="container">
        <h2 class="animate-on-scroll">À propos de Muslim Visibility</h2>
        <p class="section-subtitle animate-on-scroll">L'agence qui révolutionne le marketing d'influence éthique</p>

        <!-- Notre Histoire -->
        <div class="story-content">
          <div class="story-text">
            <h3>Notre Histoire</h3>
            <p>
              Muslim Visibility est née d'une vision : créer un pont authentique entre les marques
              et la communauté musulmane. Fondée par une équipe passionnée, notre agence s'est
              rapidement imposée comme un acteur incontournable du marketing d'influence éthique.
            </p>
            <p>
              Depuis nos débuts, nous avons accompagné des dizaines d'influenceurs et de marques
              dans des collaborations fructueuses, toujours dans le respect des valeurs et de
              l'authenticité qui nous sont chères.
            </p>
          </div>
          <div class="story-stats">
            <div class="stat-item">
              <h4>100+</h4>
              <p>Influenceurs accompagnés</p>
            </div>
            <div class="stat-item">
              <h4>50+</h4>
              <p>Marques partenaires</p>
            </div>
            <div class="stat-item">
              <h4>2M+</h4>
              <p>Portée cumulée</p>
            </div>
          </div>
        </div>


        <!-- Nos Valeurs -->
        <div class="values-section">
          <h3 class="animate-on-scroll">Nos Valeurs</h3>
          <div class="values-grid">
            <div class="value-card animate-on-scroll">
              <div class="value-icon">🤝</div>
              <h4>Éthique</h4>
              <p>
                Nous plaçons l'éthique au cœur de chaque décision, garantissant des
                collaborations respectueuses et alignées avec les valeurs de chacun.
              </p>
            </div>
            <div class="value-card animate-on-scroll">
              <div class="value-icon">💎</div>
              <h4>Transparence</h4>
              <p>
                La transparence guide toutes nos actions. Pas de surprises, pas de
                malentendus, juste une communication claire et honnête.
              </p>
            </div>
            <div class="value-card animate-on-scroll">
              <div class="value-icon">❤️</div>
              <h4>Respect</h4>
              <p>
                Le respect mutuel est la base de nos relations. Nous honorons la
                diversité culturelle et les convictions de chaque partenaire.
              </p>
            </div>
            <div class="value-card animate-on-scroll">
              <div class="value-icon">⭐</div>
              <h4>Excellence</h4>
              <p>
                Nous visons l'excellence dans chaque projet, en offrant un service
                de qualité supérieure et des résultats mesurables.
              </p>
            </div>
          </div>
        </div>

        <!-- Notre Équipe -->
        <div class="team-section">
          <h3>Notre Équipe</h3>
          <p class="team-intro">
            Une équipe diverse et expérimentée, unie par la passion de créer des
            collaborations authentiques et impactantes.
          </p>
          <div class="team-grid">
            <div class="team-member">
              <div class="member-avatar">👨‍💼</div>
              <h5>Équipe Direction</h5>
              <p>Vision stratégique et développement</p>
            </div>
            <div class="team-member">
              <div class="member-avatar">👩‍💻</div>
              <h5>Équipe Marketing</h5>
              <p>Créativité et innovation</p>
            </div>
            <div class="team-member">
              <div class="member-avatar">👨‍🤝‍👨</div>
              <h5>Équipe Relations</h5>
              <p>Accompagnement et suivi</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section class="services-section">
      <div class="container">
        <h2>Nos Services</h2>
        <div class="services-grid">
          <div class="service-item">
            <h4>Pour les Influenceurs</h4>
            <p>Développez votre audience avec des partenariats éthiques et alignés avec vos valeurs.</p>
          </div>
          <div class="service-item">
            <h4>Pour les Entreprises</h4>
            <p>Atteignez une audience engagée grâce à des collaborations authentiques et respectueuses.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact-section">
      <div class="container">
        <h2>Contactez-nous</h2>
        <p class="section-subtitle">Prêt à démarrer votre prochaine collaboration ?</p>

        <div class="contact-grid">
          <!-- Contact Info -->
          <div class="contact-info">
            <h3>Parlons de votre projet</h3>
            <p>
              Que vous soyez un influenceur à la recherche de collaborations éthiques
              ou une entreprise souhaitant toucher une audience authentique, nous sommes
              là pour vous accompagner.
            </p>

            <div class="contact-methods">
              <div class="contact-method">
                <div class="method-icon">📧</div>
                <div class="method-info">
                  <h5>Email</h5>
                  <p>contact@muslimvisibility.fr</p>
                </div>
              </div>
              <div class="contact-method">
                <div class="method-icon">📱</div>
                <div class="method-info">
                  <h5>Téléphone</h5>
                  <p>+33 1 23 45 67 89</p>
                </div>
              </div>
              <div class="contact-method">
                <div class="method-icon">💬</div>
                <div class="method-info">
                  <h5>WhatsApp</h5>
                  <p>Réponse rapide garantie</p>
                </div>
              </div>
            </div>

            <!-- WhatsApp Button -->
            <div class="whatsapp-section">
              <h4>Besoin d'une réponse rapide ?</h4>
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
              <h4>Envoyez-nous un message</h4>
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

        <!-- FAQ Section -->
        <div class="faq-section">
          <h3>Questions fréquentes</h3>
          <div class="faq-grid">
            <div class="faq-item">
              <h5>Combien de temps pour avoir une réponse ?</h5>
              <p>Nous nous engageons à répondre sous 24h en semaine, et souvent bien plus rapidement via WhatsApp.</p>
            </div>
            <div class="faq-item">
              <h5>Quels sont vos tarifs ?</h5>
              <p>Nos tarifs varient selon le type de collaboration. Contactez-nous pour un devis personnalisé et transparent.</p>
            </div>
            <div class="faq-item">
              <h5>Travaillez-vous avec tous types d'influenceurs ?</h5>
              <p>Nous travaillons avec des créateurs de contenu alignés avec nos valeurs d'éthique et d'authenticité.</p>
            </div>
            <div class="faq-item">
              <h5>Comment garantissez-vous la qualité ?</h5>
              <p>Chaque collaboration est suivie personnellement par notre équipe pour assurer des résultats optimaux.</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Final CTA Section -->
    <section class="final-cta">
      <div class="container">
        <h2>Rejoignez l'aventure</h2>
        <p>Que vous soyez influenceur ou entreprise, découvrons ensemble comment créer des collaborations qui ont du sens.</p>
        <div class="cta-buttons">
          <a href="https://wa.me/+33123456789?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services" class="btn btn-primary" target="_blank">
            Contactez-nous maintenant
          </a>
          <a href="#contact" class="btn btn-outline">
            Demander un devis
          </a>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
/* Animations */
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

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.animate-on-scroll {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease;
}

.animate-on-scroll.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.home {
  min-height: 100vh;
  background: var(--white);
  width: 100%;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

.hero {
  background: var(--gradient-primary);
  color: var(--white);
  padding: 6rem 2rem 4rem;
  text-align: center;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  scroll-margin-top: 80px;
  position: relative;
  overflow: hidden;
  width: 100%;
  margin: 0;
}


.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 80%, rgba(139, 90, 159, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(74, 144, 226, 0.3) 0%, transparent 50%);
  animation: float 6s ease-in-out infinite;
}

.hero-particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image:
    radial-gradient(2px 2px at 20px 30px, rgba(255,255,255,0.3), transparent),
    radial-gradient(2px 2px at 40px 70px, rgba(255,255,255,0.2), transparent),
    radial-gradient(1px 1px at 90px 40px, rgba(255,255,255,0.4), transparent),
    radial-gradient(1px 1px at 130px 80px, rgba(255,255,255,0.2), transparent);
  background-repeat: repeat;
  background-size: 200px 100px;
  animation: float 8s ease-in-out infinite reverse;
}

.hero-content {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.hero-title {
  font-size: 4rem;
  font-weight: 800;
  margin-bottom: 1.5rem;
  text-shadow: 0 4px 20px rgba(0,0,0,0.2);
  letter-spacing: -0.02em;
  line-height: 1.1;
}

.hero-slogan {
  font-size: 1.6rem;
  font-weight: 400;
  margin-bottom: 2rem;
  opacity: 0.95;
  letter-spacing: 0.01em;
}

.hero-description {
  font-size: 1.2rem;
  margin-bottom: 3rem;
  opacity: 0.9;
  line-height: 1.7;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 3rem;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  display: inline-block;
  padding: 1rem 2rem;
  border-radius: var(--border-radius-lg);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  border: 2px solid transparent;
  position: relative;
  overflow: hidden;
  transform: translateZ(0);
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
  transition: left 0.5s;
}

.btn:hover::before {
  left: 100%;
}

.btn-primary {
  background: var(--white);
  color: var(--primary-blue);
  box-shadow: var(--shadow-md);
}

.btn-primary:hover {
  background: var(--light-blue);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
  animation: pulse 0.6s ease-in-out;
}

.btn-secondary {
  background: transparent;
  color: var(--white);
  border: 2px solid var(--white);
}

.btn-secondary:hover {
  background: var(--white);
  color: var(--primary-blue);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

.btn-outline {
  background: transparent;
  color: var(--white);
  border: 2px solid var(--white);
}

.btn-outline:hover {
  background: var(--primary-blue);
  color: var(--white);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

.container {
  width: 100%;
  margin: 0;
  padding: 0 2rem;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

/* About Section */
.about-section {
  padding: 0;
  background: var(--white);
  scroll-margin-top: 80px;
  position: relative;
  width: 100%;
  margin: 0;
}


.about-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.about-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--black);
  position: relative;
}

.section-subtitle {
  text-align: center;
  font-size: 1.3rem;
  color: var(--medium-gray);
  margin-bottom: 4rem;
  position: relative;
}

.story-content {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 4rem;
  align-items: center;
  margin-bottom: 4rem;
}

.story-text h3 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
  color: #333;
}

.story-text p {
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 1.5rem;
  color: #666;
}

.story-stats {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.stat-item {
  text-align: center;
  padding: 2rem;
  background: var(--white);
  border-radius: var(--border-radius-lg);
  box-shadow: var(--shadow-md);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.stat-item::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--gradient-primary);
  transform: translateX(-100%);
  transition: transform 0.3s ease;
}

.stat-item:hover::before {
  transform: translateX(0);
}

.stat-item:hover {
  transform: translateY(-8px);
  box-shadow: var(--shadow-lg);
}

.stat-item h4 {
  font-size: 2.5rem;
  font-weight: 700;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.stat-item p {
  color: var(--medium-gray);
  font-weight: 500;
  margin: 0;
}


.values-section {
  margin-bottom: 4rem;
}

.values-section h3 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 2rem;
  color: #333;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.value-card {
  background: var(--white);
  padding: 2.5rem 2rem;
  border-radius: var(--border-radius-lg);
  box-shadow: var(--shadow-md);
  text-align: center;
  transition: all 0.4s ease;
  position: relative;
  overflow: hidden;
  border: 1px solid transparent;
}

.value-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--gradient-secondary);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.value-card::after {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: var(--gradient-primary);
  border-radius: var(--border-radius-lg);
  z-index: -1;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.value-card:hover {
  transform: translateY(-10px) scale(1.02);
  box-shadow: var(--shadow-lg);
}

.value-card:hover::before {
  opacity: 0.05;
}

.value-card:hover::after {
  opacity: 1;
}

.value-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  transition: transform 0.3s ease;
}

.value-card:hover .value-icon {
  transform: scale(1.1) rotate(5deg);
}

.value-card h4 {
  font-size: 1.4rem;
  margin-bottom: 1rem;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  position: relative;
  transition: color 0.3s ease, -webkit-text-fill-color 0.3s ease;
}

.value-card p {
  color: var(--medium-gray);
  line-height: 1.6;
  margin: 0;
  position: relative;
  transition: color 0.3s ease;
}

.value-card:hover h4 {
  -webkit-text-fill-color: var(--white);
  color: var(--white);
}

.value-card:hover p {
  color: var(--white);
}

.team-section h3 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 1rem;
  color: #333;
}

.team-intro {
  text-align: center;
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 2rem;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
}

.team-member {
  text-align: center;
  padding: 2rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.team-member:hover {
  transform: translateY(-5px);
}

.member-avatar {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.team-member h5 {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #333;
}

.team-member p {
  color: #666;
  margin: 0;
}

/* Services Section */
.services-section {
  padding: 0;
  background: var(--gradient-primary);
  position: relative;
  width: 100%;
  margin: 0;
}


.services-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.services-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: var(--white);
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
}

.service-item {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  text-align: center;
  transition: transform 0.3s ease;
}

.service-item:hover {
  transform: translateY(-5px);
}

.service-item h4 {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: #2c5aa0;
}

.service-item p {
  color: #666;
  line-height: 1.6;
  margin: 0;
}

/* Contact Section */
.contact-section {
  padding: 0;
  background: var(--white);
  scroll-margin-top: 80px;
  position: relative;
  width: 100%;
  margin: 0;
  color: var(--black);
}

.contact-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.contact-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--black);
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
  margin-bottom: 4rem;
}

.contact-info h3 {
  font-size: 1.8rem;
  margin-bottom: 1.5rem;
  color: var(--black);
}

.contact-info > p {
  font-size: 1.1rem;
  color: var(--medium-gray);
  line-height: 1.6;
  margin-bottom: 2rem;
}

.contact-methods {
  margin-bottom: 2rem;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
  padding: 1rem;
  background: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.method-icon {
  font-size: 1.5rem;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f0f7ff;
  border-radius: 50%;
}

.method-info h5 {
  margin-bottom: 0.3rem;
  color: var(--black);
}

.method-info p {
  color: var(--medium-gray);
  margin: 0;
}

.whatsapp-section {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  text-align: center;
}

.whatsapp-section h4 {
  margin-bottom: 1rem;
  color: var(--black);
}

.whatsapp-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  background: linear-gradient(135deg, #25D366 0%, #20B954 100%);
  color: var(--white);
  padding: 1.2rem 2.5rem;
  border-radius: var(--border-radius-lg);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  font-size: 1.1rem;
  box-shadow: var(--shadow-md);
  position: relative;
  overflow: hidden;
}

.whatsapp-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
  transition: left 0.5s;
}

.whatsapp-btn:hover::before {
  left: 100%;
}

.whatsapp-btn:hover {
  background: linear-gradient(135deg, #20B954 0%, #1da848 100%);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
  animation: pulse 0.6s ease-in-out;
}

.whatsapp-icon {
  font-size: 1.3rem;
  animation: float 2s ease-in-out infinite;
}

.form-card {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.form-card h4 {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: #333;
  text-align: center;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
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
  padding: 0.8rem;
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
  min-height: 100px;
}

.submit-btn {
  background: #2c5aa0;
  color: white;
  border: none;
  padding: 1rem 2rem;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-top: 1rem;
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
  margin-top: 1rem;
}

.faq-section {
  margin-top: 4rem;
}

.faq-section h3 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 2rem;
  color: var(--black);
}

.faq-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

.faq-item {
  background: white;
  padding: 1.5rem;
  border-radius: 15px;
  border-left: 4px solid #2c5aa0;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.faq-item h5 {
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
  color: #333;
}

.faq-item p {
  color: #666;
  line-height: 1.6;
  margin: 0;
}

/* Final CTA Section */
.final-cta {
  background: var(--gradient-primary);
  color: var(--white);
  padding: 0;
  text-align: center;
  position: relative;
  overflow: hidden;
  width: 100%;
  margin: 0;
}

.final-cta .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.final-cta::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 30% 20%, rgba(255,255,255,0.1) 0%, transparent 50%),
    radial-gradient(circle at 70% 80%, rgba(255,255,255,0.05) 0%, transparent 50%);
}


.final-cta h2 {
  font-size: 2.8rem;
  margin-bottom: 1rem;
  position: relative;
  z-index: 2;
}

.final-cta p {
  font-size: 1.3rem;
  margin-bottom: 2.5rem;
  opacity: 0.95;
  position: relative;
  z-index: 2;
}

.cta-buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  flex-wrap: wrap;
  position: relative;
  z-index: 2;
}

@media (max-width: 768px) {
  .hero {
    padding: 4rem 1rem 3rem;
  }

  .hero-title {
    font-size: 2rem;
  }

  .hero-slogan {
    font-size: 1.1rem;
  }

  .hero-description {
    font-size: 1rem;
  }

  .container {
    padding: 0 1rem;
  }

  .btn {
    width: 100%;
    max-width: 300px;
  }

  /* About Section Mobile */
  .story-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .story-stats {
    flex-direction: row;
    justify-content: space-around;
    flex-wrap: wrap;
  }

  .stat-item {
    flex: 1;
    margin: 0 0.5rem;
    min-width: 100px;
    padding: 1.5rem 1rem;
  }

  .stat-item h4 {
    font-size: 1.8rem;
  }

  .stat-item p {
    font-size: 0.9rem;
  }

  .values-grid,
  .team-grid {
    grid-template-columns: 1fr;
  }

  /* Réduction des tailles de texte */
  .about-section h2,
  .services-section h2,
  .contact-section h2,
  .faq-section h2 {
    font-size: 2rem;
  }

  .value-card h4,
  .service-item h4,
  .team-member h4 {
    font-size: 1.2rem;
  }

  .value-card p,
  .service-item p,
  .story-text p,
  .team-member p,
  .section-subtitle {
    font-size: 0.95rem;
  }

  .faq-item h4 {
    font-size: 1.1rem;
  }

  .faq-item p {
    font-size: 0.9rem;
  }

  /* Services Section Mobile */
  .services-grid {
    grid-template-columns: 1fr;
  }

  /* Contact Section Mobile */
  .contact-grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .contact-method {
    flex-direction: column;
    text-align: center;
    padding: 1.5rem;
  }

  .method-icon {
    margin-bottom: 0.5rem;
  }

  .faq-grid {
    grid-template-columns: 1fr;
  }

  .form-card {
    padding: 1.5rem;
  }

  .whatsapp-section {
    padding: 1.5rem;
  }
}

/* Media query pour très petits écrans */
@media (max-width: 480px) {
  .hero {
    padding: 3rem 1rem 2rem;
  }

  .hero-title {
    font-size: 1.8rem;
    margin-bottom: 1rem;
  }

  .hero-slogan {
    font-size: 1rem;
    margin-bottom: 1.5rem;
  }

  .hero-description {
    font-size: 0.9rem;
    margin-bottom: 2rem;
  }

  .story-content {
    gap: 1.5rem;
  }

  .story-text h3 {
    font-size: 1.6rem;
    text-align: center;
  }

  .story-text p {
    font-size: 1rem;
    text-align: center;
  }

  .story-stats {
    flex-direction: column;
    gap: 1rem;
  }

  .stat-item {
    margin: 0;
    padding: 1.2rem 0.8rem;
    min-width: auto;
  }

  .stat-item h4 {
    font-size: 1.5rem;
  }

  .stat-item p {
    font-size: 0.85rem;
  }

  /* Réduction supplémentaire des tailles de texte pour très petits écrans */
  .about-section h2,
  .services-section h2,
  .contact-section h2,
  .faq-section h2 {
    font-size: 1.8rem;
  }

  .value-card h4,
  .service-item h4,
  .team-member h4 {
    font-size: 1.1rem;
  }

  .value-card p,
  .service-item p,
  .story-text p,
  .team-member p,
  .section-subtitle {
    font-size: 0.85rem;
  }

  .faq-item h4 {
    font-size: 1rem;
  }

  .faq-item p {
    font-size: 0.8rem;
  }

  .contact-info h3,
  .form-card h4 {
    font-size: 1.2rem;
  }

  .method-info h5 {
    font-size: 0.9rem;
  }

  .method-info p {
    font-size: 0.8rem;
  }
}
</style>
