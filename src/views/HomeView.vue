<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const form = ref({
  name: '',
  email: '',
  type: '',
  phone: '',
  message: ''
})

const isSubmitting = ref(false)
const submitted = ref(false)
const testimonialSlider = ref<HTMLElement>()
const brandsSlider = ref<HTMLElement>()

// Système de filtrage des offres
const activeOfferCategory = ref('publicite')

// Système de carrousel pour mobile
const currentSlidePublicite = ref(0)
const currentSlideAbonnement = ref(0)
const currentSlidePrestations = ref(0)

// Système d'accordéon FAQ
const openFaqIndex = ref<number | null>(null)

const toggleFaq = (index: number) => {
  if (openFaqIndex.value === index) {
    openFaqIndex.value = null
  } else {
    openFaqIndex.value = index
  }
}

const scrollToSlide = (category: string, direction: 'next' | 'prev') => {
  const container = document.querySelector(`[data-category="${category}"]`) as HTMLElement
  if (!container) return

  const cards = container.querySelectorAll('.offer-card')
  const cardWidth = (cards[0] as HTMLElement).offsetWidth
  const gap = 24 // 1.5rem = 24px

  let currentSlide = 0
  if (category === 'publicite') {
    currentSlide = currentSlidePublicite.value
  } else if (category === 'abonnement') {
    currentSlide = currentSlideAbonnement.value
  } else if (category === 'prestations') {
    currentSlide = currentSlidePrestations.value
  }

  if (direction === 'next') {
    currentSlide = Math.min(currentSlide + 1, cards.length - 1)
  } else {
    currentSlide = Math.max(currentSlide - 1, 0)
  }

  if (category === 'publicite') {
    currentSlidePublicite.value = currentSlide
  } else if (category === 'abonnement') {
    currentSlideAbonnement.value = currentSlide
  } else if (category === 'prestations') {
    currentSlidePrestations.value = currentSlide
  }

  const scrollPosition = currentSlide * (cardWidth + gap)
  container.scrollTo({
    left: scrollPosition,
    behavior: 'smooth'
  })
}

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

let testimonialInterval: number
let brandInterval: number

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

  // Auto-slider pour les témoignages - toutes les 5 secondes, défilement plus lent
  if (testimonialSlider.value) {
    let currentTestimonial = 0
    const testimonialCards = testimonialSlider.value.querySelectorAll('.testimonial-card')

    testimonialInterval = setInterval(() => {
      currentTestimonial = (currentTestimonial + 1) % testimonialCards.length
      const offset = currentTestimonial * -20 // -20% pour chaque slide (5 slides = 100%)
      testimonialSlider.value!.style.transform = `translateX(${offset}%)`
    }, 5000) // Augmenté à 5 secondes
  }

  // Auto-slider pour les marques - défilement continu
  if (brandsSlider.value) {
    let brandOffset = 0
    const brandWidth = 200 // Largeur approximative d'un logo + gap

    brandInterval = setInterval(() => {
      brandOffset -= 1
      // Reset quand on a fait défiler 4 logos (pour garder 3 visibles)
      if (Math.abs(brandOffset) >= brandWidth * 4) {
        brandOffset = 0
      }
      brandsSlider.value!.style.transform = `translateX(${brandOffset}px)`
    }, 30) // Animation fluide
  }
})

onUnmounted(() => {
  if (testimonialInterval) {
    clearInterval(testimonialInterval)
  }
  if (brandInterval) {
    clearInterval(brandInterval)
  }
})
</script>

<template>
  <div class="home">
    <!-- Hero Section -->
    <section id="accueil" class="hero">
      <video autoplay muted loop playsinline class="hero-video">
        <source src="/herovideo.mp4" type="video/mp4">
        Votre navigateur ne supporte pas la vidéo.
      </video>
      <div class="hero-background"></div>
      <div class="hero-content">
        <div class="hero-layout">
          <div class="hero-text">
            <h1 class="hero-title animate-on-scroll">Muslim Visibility</h1>
            <p class="hero-slogan animate-on-scroll">Votre succès, notre engagement éthique</p>
            <p class="hero-description animate-on-scroll">
              Votre entreprise mérite d'être vue. Muslim Visibility est là pour ça.
            </p>
          </div>
          <div class="hero-actions animate-on-scroll">
            <a href="https://wa.me/+33618937532?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services" class="btn btn-primary" target="_blank">
              💬 Nous contacter sur WhatsApp
            </a>
            <a href="https://wa.me/+33618937532?text=Bonjour%2C%20je%20souhaite%20demander%20un%20devis" class="btn btn-primary" target="_blank">
              Demander un devis
            </a>
          </div>
        </div>
      </div>
      <div class="hero-particles"></div>
    </section>

    <!-- About Section -->
    <section id="about" class="about-section">
      <div class="container">
        <h2 class="animate-on-scroll">À propos de Muslim Visibility</h2>
        <p class="section-subtitle animate-on-scroll">L'agence qui révolutionne le marketing d'influence éthique</p>

        <!-- Qui sommes-nous -->
        <div class="story-content">
          <div class="story-text">
            <h3>Qui sommes-nous</h3>
            <p>
              Nous accompagnons les entrepreneurs et commerçants souhaitant atteindre efficacement la communauté musulmane.
            </p>
            <p>
              Nous travaillons en collaboration avec des influenceurs et des pages à forte visibilité, ciblant spécifiquement la communauté musulmane sur Instagram, mais également sur Facebook, TikTok et d'autres plateformes.
            </p>
            <p>
              Grâce à ces partenariats, nous offrons des campagnes publicitaires performantes et un marketing d'influence éthique pour maximiser l'impact de vos actions.
            </p>
          </div>
          <div class="story-stats">
            <div class="stat-item">
              <h4>+40</h4>
              <p>Partenaires influents</p>
            </div>
            <div class="stat-item">
              <h4>+4M</h4>
              <p>Visibilité cumulée</p>
            </div>
            <div class="stat-item">
              <h4>+700</h4>
              <p>Publicités réalisées</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Nos Valeurs Section -->
    <section class="values-section">
      <div class="container">
        <h2 class="animate-on-scroll">Nos Valeurs</h2>
        <p class="section-subtitle animate-on-scroll">Les principes qui guident nos actions</p>

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
            <div class="value-icon">🌟</div>
            <h4>Valorisation</h4>
            <p>
              Nous aidons les commerçants, marques et prestataires musulmans à gagner en visibilité et en reconnaissance, tout en valorisant leurs produits et services dans le monde digital.
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
    </section>

    <!-- Nos Offres Section -->
    <section id="offres" class="offers-section">
      <div class="container">
        <h2 class="animate-on-scroll">Nos Offres</h2>
        <p class="section-subtitle animate-on-scroll">
          Choisissez la formule adaptée à vos besoins et donnez de la visibilité à votre projet grâce à Muslim Visibility.
        </p>

        <!-- Filter Buttons -->
        <div class="offers-filter">
          <button
            class="filter-btn"
            :class="{ active: activeOfferCategory === 'publicite' }"
            @click="activeOfferCategory = 'publicite'"
          >
            📢 Formules Publicitaires
          </button>
          <button
            class="filter-btn"
            :class="{ active: activeOfferCategory === 'prestations' }"
            @click="activeOfferCategory = 'prestations'"
          >
            🎨 Autres Prestations
          </button>
        </div>

        <!-- Formules Publicitaires -->
        <div
          v-show="activeOfferCategory === 'publicite'"
          class="offers-grid"
          data-category="publicite"
        >
          <!-- OneShot -->
          <div class="offer-card animate-on-scroll">
            <div class="offer-header">
              <h3>OneShot</h3>
              <div class="offer-badge">Test ponctuel</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                La formule la plus économique, idéale pour tester la publicité de votre produit ou service.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>1 story chez un(e) partenaire ou influenceur(se)</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Test ponctuel sans engagement</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Idéal pour découvrir l'impact d'une publicité ciblée</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Accessible dès 10 €</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Durée :</strong> ponctuelle
                </div>
                <div class="meta-item">
                  <strong>Engagement :</strong> sans engagement
                </div>
              </div>
            </div>
          </div>

          <!-- Short Campaign -->
          <div class="offer-card animate-on-scroll featured">
            <div class="offer-badge-featured">Populaire</div>
            <div class="offer-header">
              <h3>Short Campaign</h3>
              <div class="offer-badge">Lancement rapide</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                Idéal pour un lancement rapide, une mise en avant ponctuelle ou une promotion en cours.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Diffusion de votre publicité en story Instagram</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Possible aussi sur Snapchat, TikTok ou autres réseaux (sur demande et devis personnalisé)</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Idéal pour les promotions, offres spéciales ou événements particuliers</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Accessible dès 80 € de budget</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Durée :</strong> campagne courte (quelques jours à 2 semaines)
                </div>
                <div class="meta-item">
                  <strong>Engagement :</strong> sans engagement
                </div>
              </div>
            </div>
          </div>

          <!-- ABO+ -->
          <div class="offer-card animate-on-scroll">
            <div class="offer-header">
              <h3>ABO+</h3>
              <div class="offer-badge">Formule complète et stable</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                Une formule complète et stable sur 3 mois.
              </p>
              <p class="offer-intro">
                Avec l'ABO+, tu choisis un ou plusieurs partenaires (influenceurs ou pages à forte visibilité) avec lesquels tu t'engages sur toute la durée.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Chaque partenaire diffuse 2 posts et 5 stories par mois</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Conception visuelle incluse</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Scripts optimisés inclus</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Rapport d'analyse inclus</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Une stratégie continue pour installer ta marque et créer une vraie relation de confiance avec ton audience</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Tarif :</strong> à partir de 180€/mois
                </div>
                <div class="meta-item">
                  <strong>Durée :</strong> 3 mois d'engagement
                </div>
              </div>
            </div>
          </div>

          <!-- ABO FLEX -->
          <div class="offer-card animate-on-scroll">
            <div class="offer-header">
              <h3>🔁 ABO FLEX</h3>
              <div class="offer-badge">Formule flexible</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                Une formule plus souple, toujours sur 3 mois d'accompagnement, mais avec la liberté de changer de partenaire chaque mois.
              </p>
              <p class="offer-intro">
                Tu profites de la même qualité de contenu et de stratégie qu'en ABO+, tout en variant les profils d'influenceurs pour toucher différents publics.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Liberté de changer de partenaire chaque mois</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Même qualité de contenu qu'en ABO+</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Stratégie continue sur 3 mois</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Idéal pour tester, ajuster et maximiser ta visibilité</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Tarif :</strong> à partir de 180€/mois + option Flex 100€ (une seule fois)
                </div>
                <div class="meta-item">
                  <strong>Durée :</strong> 3 mois d'accompagnement
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Autres Prestations -->
        <div
          v-show="activeOfferCategory === 'prestations'"
          class="offers-grid"
          data-category="prestations"
        >
          <!-- Community Management -->
          <div class="offer-card animate-on-scroll">
            <div class="offer-header">
              <h3>Community Management</h3>
              <div class="offer-badge">Gestion complète</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                Confiez-nous la gestion de vos réseaux sociaux pour une présence régulière et professionnelle.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Gestion de vos comptes (posts, stories, interaction)</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Stratégie éditoriale adaptée à vos objectifs</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Suivi et optimisation des performances</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Tarif :</strong> sur devis (selon vos besoins et vos objectifs)
                </div>
              </div>
            </div>
          </div>

          <!-- Création Visuelle -->
          <div class="offer-card animate-on-scroll">
            <div class="offer-header">
              <h3>Création Visuelle</h3>
              <div class="offer-badge">Design professionnel</div>
            </div>
            <div class="offer-description">
              <p class="offer-intro">
                Des visuels attractifs et professionnels pour mettre en valeur vos produits et services.
              </p>
            </div>
            <div class="offer-features">
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Flyers</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Réels Instagram</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Carrousels</span>
              </div>
              <div class="feature-item">
                <span class="feature-icon">✅</span>
                <span>Autres visuels adaptés aux réseaux sociaux</span>
              </div>
            </div>
            <div class="offer-footer">
              <div class="offer-meta">
                <div class="meta-item">
                  <strong>Tarif :</strong> à partir de 20 € / visuel
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- CTA Button -->
        <div class="offers-cta">
          <a href="#contact" class="btn btn-primary">Demander un devis personnalisé</a>
        </div>
      </div>
    </section>

    <!-- Ils nous font confiance Section -->
    <section class="trusted-brands-section">
      <div class="container">
        <h2 class="animate-on-scroll">Ils nous font confiance</h2>
        <p class="section-subtitle animate-on-scroll">Des marques de renom qui partagent nos valeurs</p>

        <div class="brands-slider-wrapper">
          <div class="brands-slider" ref="brandsSlider">
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.29.26_1ce76da0.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.34.44_dab1cd9a.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.37.59_6795c4da.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.39.19_413669a0.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.40.41_41138365.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.41.19_b538ba65.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.43.27_566db64d.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.44.27_a2a59e11.jpg" alt="Brand Logo" />
            </div>
            <div class="brand-logo">
              <img src="/WhatsApp Image 2025-10-23 à 15.47.54_c7be75f2.jpg" alt="Brand Logo" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Commentaires Section -->
    <section class="testimonials-section">
      <div class="container">
        <h2 class="animate-on-scroll">Ce que disent nos clients</h2>
        <p class="section-subtitle animate-on-scroll">Leurs témoignages parlent pour nous</p>

        <div class="testimonials-container">
          <div class="testimonials-slider" ref="testimonialSlider">
            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="stars">⭐⭐⭐⭐⭐</div>
                <p>"Muslim Visibility a transformé ma carrière d'influenceuse. Grâce à eux, j'ai trouvé des collaborations authentiques qui correspondent parfaitement à mes valeurs. L'équipe est professionnelle et à l'écoute."</p>
                <div class="testimonial-author">
                  <div class="author-avatar">👩‍🦱</div>
                  <div class="author-info">
                    <h5>Amina L.</h5>
                    <span>Influenceuse lifestyle</span>
                  </div>
                </div>
              </div>
            </div>

            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="stars">⭐⭐⭐⭐⭐</div>
                <p>"En tant qu'entreprise, nous cherchions des influenceurs authentiques pour promouvoir nos produits halal. Muslim Visibility nous a connectés avec des créateurs parfaits pour notre marque. ROI exceptionnel !"</p>
                <div class="testimonial-author">
                  <div class="author-avatar">👨‍💼</div>
                  <div class="author-info">
                    <h5>Karim B.</h5>
                    <span>Directeur Marketing</span>
                  </div>
                </div>
              </div>
            </div>

            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="stars">⭐⭐⭐⭐⭐</div>
                <p>"J'ai enfin trouvé une agence qui comprend mes valeurs ! Les collaborations proposées sont toujours en adéquation avec mon contenu et mon audience. Je recommande vivement Muslim Visibility."</p>
                <div class="testimonial-author">
                  <div class="author-avatar">🧕</div>
                  <div class="author-info">
                    <h5>Fatima K.</h5>
                    <span>Content Creator</span>
                  </div>
                </div>
              </div>
            </div>

            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="stars">⭐⭐⭐⭐⭐</div>
                <p>"Transparence, professionnalisme et respect : voilà ce qui définit Muslim Visibility. Ils ont su nous accompagner dans notre stratégie d'influence avec une approche éthique remarquable."</p>
                <div class="testimonial-author">
                  <div class="author-avatar">👩‍💻</div>
                  <div class="author-info">
                    <h5>Sarah M.</h5>
                    <span>Responsable Communication</span>
                  </div>
                </div>
              </div>
            </div>

            <div class="testimonial-card">
              <div class="testimonial-content">
                <div class="stars">⭐⭐⭐⭐⭐</div>
                <p>"Muslim Visibility m'a aidé à développer mon audience de manière authentique. Les partenariats qu'ils proposent sont toujours de qualité et respectent mes convictions. Une équipe fantastique !"</p>
                <div class="testimonial-author">
                  <div class="author-avatar">👨‍🎨</div>
                  <div class="author-info">
                    <h5>Omar T.</h5>
                    <span>Créateur de contenu</span>
                  </div>
                </div>
              </div>
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
            <p>Tu es influenceur, influenceuse ou tu gères une page à forte visibilité ?<br>
            Muslim Visibility recrute des partenaires pour collaborer sur des campagnes rémunérées et aider les commerçants et prestataires musulmans à se développer.</p>
            <p>Si tu veux participer à la croissance de la communauté tout en valorisant ton audience, contacte-nous dès maintenant.</p>
          </div>
          <div class="service-item">
            <h4>Pour les Professionnels</h4>
            <p>Vous êtes commerçant, marque ou prestataire de services ?<br>
            Muslim Visibility vous aide à promouvoir vos produits et services à travers un réseau d'influenceurs qualifiés et engagés.<br>
            Profitez d'une visibilité ciblée et authentique au sein de la communauté musulmane, et développez votre notoriété en ligne.</p>
            <p>Contactez-nous pour élaborer ensemble votre prochaine campagne.</p>
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
                  <p>+33 6 18 93 75 32</p>
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
              <a href="https://wa.me/+33618937532?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services"
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
                    <option value="professionnel">Professionnel</option>
                    <option value="autre">Autre</option>
                  </select>
                </div>

                <div class="form-group">
                  <label for="phone">Téléphone (optionnel)</label>
                  <input
                    type="tel"
                    id="phone"
                    v-model="form.phone"
                    placeholder="+33 6 18 93 75 32"
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
          <h3>Foire aux Questions</h3>
          <div class="faq-accordion">
            <div class="faq-item" :class="{ open: openFaqIndex === 0 }" @click="toggleFaq(0)">
              <div class="faq-question">
                <h5>1. Qu'est-ce que Muslim Visibility ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 0 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Muslim Visibility est une agence spécialisée dans la publicité d'influence et la visibilité digitale dédiée aux commerçants, marques et prestataires musulmans. Nous mettons en relation les entreprises avec des influenceurs fiables et alignés sur nos valeurs pour promouvoir leurs produits et services.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 1 }" @click="toggleFaq(1)">
              <div class="faq-question">
                <h5>2. Quels types d'offres propose Muslim Visibility ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 1 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Nous proposons plusieurs formules selon tes besoins : OneShot (collaboration ponctuelle), ShortCampaign (campagne rapide), ABO+ (accompagnement sur 3 mois), et ABO FLEX (abonnement 3 mois avec changement de partenaire possible). Chaque formule s'adapte à ton budget, ton objectif et ton rythme de communication.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 2 }" @click="toggleFaq(2)">
              <div class="faq-question">
                <h5>3. Comment fonctionne une campagne ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 2 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Nous sélectionnons les partenaires (pages ou influenceurs) les plus adaptés à ton activité, concevons les visuels et les scripts, puis diffusons la campagne selon une stratégie sur mesure. Un rapport d'analyse est ensuite remis à la fin de la période.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 3 }" @click="toggleFaq(3)">
              <div class="faq-question">
                <h5>4. Combien coûtent les campagnes et abonnements ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 3 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Les formules ABO+ et ABO FLEX commencent à partir de 180€/mois (sur 3 mois). L'option Flex est facturée 100€ une seule fois. Les formules OneShot et ShortCampaign sont tarifées à la carte, selon la visibilité et le nombre de partenaires choisis.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 4 }" @click="toggleFaq(4)">
              <div class="faq-question">
                <h5>5. Comment se font les paiements ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 4 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Les règlements peuvent se faire par virement bancaire ou via PayPal, selon ce qui t'arrange le mieux. Les paiements sont effectués en début de prestation, conformément au devis validé.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 5 }" @click="toggleFaq(5)">
              <div class="faq-question">
                <h5>6. Qu'est-ce que comprend une campagne ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 5 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Chaque partenaire diffuse en moyenne 2 posts et 5 stories par mois, avec la création visuelle offerte, les scripts optimisés et un rapport d'analyse détaillé. Les formats varient selon la formule choisie (Story simple, Story facecam, ou Réel cross-sharing).</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 6 }" @click="toggleFaq(6)">
              <div class="faq-question">
                <h5>7. Puis-je choisir mes influenceurs ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 6 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Oui, tu peux proposer un ou plusieurs profils que tu souhaites cibler, ou laisser notre équipe te recommander les meilleurs partenaires selon ton domaine et ton budget.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 7 }" @click="toggleFaq(7)">
              <div class="faq-question">
                <h5>8. Est-ce réservé uniquement aux marques musulmanes ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 7 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Nous mettons en avant principalement les entreprises, prestataires et projets éthiques partageant des valeurs compatibles avec la communauté musulmane.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 8 }" @click="toggleFaq(8)">
              <div class="faq-question">
                <h5>9. Comment devenir partenaire ou influenceur chez Muslim Visibility ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 8 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Si tu es influenceur, influenceuse ou que tu gères une page à forte visibilité, tu peux nous contacter via le formulaire de collaboration. Nos équipes étudieront ton profil pour rejoindre notre réseau et participer à des campagnes rémunérées.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 9 }" @click="toggleFaq(9)">
              <div class="faq-question">
                <h5>10. Proposez-vous aussi de la gestion de réseaux sociaux ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 9 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Oui. Nous proposons des services de Community Management, de création visuelle (flyers, reels, carrousels) et d'accompagnement stratégique personnalisés, en dehors des formules publicitaires.</p>
              </div>
            </div>

            <div class="faq-item" :class="{ open: openFaqIndex === 10 }" @click="toggleFaq(10)">
              <div class="faq-question">
                <h5>11. Comment vous contacter ?</h5>
                <span class="faq-icon">{{ openFaqIndex === 10 ? '−' : '+' }}</span>
              </div>
              <div class="faq-answer">
                <p>Tu peux nous écrire directement via le formulaire de contact du site, par e-mail à muslimvisibility@gmail.com, ou nous joindre au 07 61 06 64 91 (disponible aussi sur WhatsApp). Nous répondons généralement sous 24 à 48 heures.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Final CTA Section -->
    <section class="final-cta">
      <div class="container">
        <h2>Rejoignez l'aventure</h2>
        <p>Que vous soyez influenceur ou professionnel, découvrons ensemble comment créer des collaborations qui ont du sens.</p>
        <div class="cta-buttons">
          <a href="https://wa.me/+33618937532?text=Bonjour%2C%20je%20souhaite%20en%20savoir%20plus%20sur%20vos%20services" class="btn btn-primary" target="_blank">
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
  color: var(--white);
  padding: 6rem 2rem 4rem;
  text-align: left;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: flex-start;
  scroll-margin-top: 80px;
  position: relative;
  overflow: hidden;
  width: 100%;
  margin: 0;
}

.hero-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}


.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 1;
}

@keyframes modernFloat {
  0%, 100% {
    transform: translate(0px, 0px) scale(1);
  }
  25% {
    transform: translate(20px, -15px) scale(1.05);
  }
  50% {
    transform: translate(-10px, 10px) scale(0.98);
  }
  75% {
    transform: translate(15px, -5px) scale(1.02);
  }
}

.hero-particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image:
    radial-gradient(circle 1px at 20% 30%, rgba(255, 255, 255, 0.3), transparent),
    radial-gradient(circle 0.5px at 60% 20%, rgba(255, 255, 255, 0.2), transparent),
    radial-gradient(circle 1px at 80% 70%, rgba(255, 255, 255, 0.25), transparent),
    radial-gradient(circle 0.5px at 30% 80%, rgba(255, 255, 255, 0.15), transparent);
  background-repeat: repeat;
  background-size: 400px 300px;
  animation: particleFloat 30s linear infinite;
  opacity: 0.6;
}

@keyframes particleFloat {
  0% {
    transform: translateY(0px);
  }
  100% {
    transform: translateY(-20px);
  }
}


.hero-content {
  max-width: 1400px;
  margin: 0;
  position: relative;
  z-index: 10;
  padding-left: 4rem;
  width: 100%;
}

.hero-layout {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 4rem;
  width: 100%;
}

.hero-text {
  flex: 1;
  max-width: 50%;
  width: 50%;
}

.hero-title {
  font-size: 5rem;
  font-weight: 800;
  margin-bottom: 1.5rem;
  color: var(--white);
  text-shadow: 0 4px 20px rgba(0,0,0,0.3);
  letter-spacing: -0.02em;
  line-height: 1.1;
  position: relative;
  z-index: 3;
}

.hero-slogan {
  font-size: 2rem;
  font-weight: 400;
  margin-bottom: 2rem;
  color: var(--white);
  opacity: 0.95;
  letter-spacing: 0.01em;
  position: relative;
  z-index: 3;
}

.hero-description {
  font-size: 1.4rem;
  margin-bottom: 3rem;
  color: var(--white);
  opacity: 0.9;
  line-height: 1.7;
  max-width: 80%;
  margin-left: 0;
  margin-right: auto;
  margin-bottom: 3rem;
  position: relative;
  z-index: 3;
}

.hero-actions {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: flex-start;
  position: relative;
  z-index: 3;
  flex-shrink: 0;
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
  color: var(--secondary-blue);
  box-shadow: var(--shadow-md);
  border: 2px solid var(--white);
  position: relative;
  overflow: hidden;
}

.btn-primary::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--gradient-primary);
  transition: left 0.3s ease;
  z-index: -1;
}

.btn-primary:hover {
  background: transparent;
  color: var(--white);
  border-color: var(--white);
  transform: translateY(-3px);
  box-shadow: var(--shadow-lg);
}

.btn-primary:hover::before {
  left: 0;
}

.btn-secondary {
  background: transparent;
  color: var(--white);
  border: 2px solid var(--white);
}

.btn-secondary:hover {
  background: var(--white);
  color: var(--secondary-blue);
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
}

.btn-outline {
  background: transparent;
  color: var(--white);
  border: 2px solid var(--white);
}

.btn-outline:hover {
  background: var(--gradient-primary);
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
  color: var(--black);
}

.story-text p {
  font-size: 1.1rem;
  line-height: 1.7;
  margin-bottom: 1.5rem;
  color: var(--medium-gray);
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
  padding: 0;
  background: var(--gradient-primary);
  position: relative;
  width: 100%;
  margin: 0;
}

.values-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.values-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--white);
}

.values-section .section-subtitle {
  color: var(--white);
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

.value-card:hover {
  background: var(--gradient-primary);
  color: var(--white);
}

/* Testimonials Section */
.testimonials-section {
  padding: 0;
  background: var(--light-gray);
  position: relative;
  width: 100%;
  margin: 0;
}

.testimonials-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.testimonials-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--black);
}

.testimonials-container {
  max-width: 800px;
  margin: 0 auto;
  overflow: hidden;
  border-radius: var(--border-radius-lg);
  position: relative;
  background: var(--light-gray);

}

.testimonials-slider {
  display: flex;
  transition: transform 1s ease-in-out;
  width: 500%; /* 5 témoignages */
}

.testimonial-card {
  flex: 0 0 20%; /* 100% / 5 témoignages */
  padding: 0 1rem;
}

.testimonial-content {
  background: var(--white);
  padding: 2.5rem;
  border-radius: var(--border-radius-lg);
  text-align: center;
  position: relative;
  overflow: hidden;
}

.testimonial-content::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--gradient-primary);
}

.stars {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: #FFD700;
}

.testimonial-content p {
  font-size: 1.1rem;
  line-height: 1.7;
  color: var(--medium-gray);
  margin-bottom: 2rem;
  font-style: italic;
}

.testimonial-author {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.author-avatar {
  font-size: 3rem;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--light-blue);
  border-radius: 50%;
  flex-shrink: 0;
}

.author-info h5 {
  margin: 0 0 0.2rem 0;
  color: var(--black);
  font-weight: 600;
  font-size: 1.1rem;
}

.author-info span {
  color: var(--medium-gray);
  font-size: 0.9rem;
}

/* Trusted Brands Section */
.trusted-brands-section {
  padding: 0;
  background: var(--white);
  position: relative;
  width: 100%;
  margin: 0;
}

.trusted-brands-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.trusted-brands-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--black);
}

.brands-slider-wrapper {
  margin-top: 3rem;
  overflow: hidden;
  position: relative;
}

.brands-slider-wrapper::before,
.brands-slider-wrapper::after {
  content: '';
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100px;
  z-index: 2;
  pointer-events: none;
}

.brands-slider-wrapper::before {
  left: 0;
  background: linear-gradient(to right, var(--white), transparent);
}

.brands-slider-wrapper::after {
  right: 0;
  background: linear-gradient(to left, var(--white), transparent);
}

.brands-slider {
  display: flex;
  gap: 2rem;
  width: max-content;
  transition: transform 0.03s linear;
}

.brand-logo {
  flex: 0 0 180px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.brand-logo img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: var(--border-radius);
  background: var(--white);
  padding: 1rem;
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
}

.brand-logo img:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-5px);
}

.logo-placeholder {
  background: var(--white);
  border: 2px solid var(--light-gray);
  border-radius: var(--border-radius);
  padding: 1.5rem;
  text-align: center;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  box-shadow: var(--shadow-sm);
}

.logo-placeholder:hover {
  border-color: var(--primary-blue);
  box-shadow: var(--shadow-md);
  transform: translateY(-5px);
}

.logo-placeholder span {
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.logo-placeholder h4 {
  font-size: 0.9rem;
  color: var(--medium-gray);
  margin: 0;
  font-weight: 500;
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
  color: var(--black);
}

.service-item p {
  color: var(--medium-gray);
  line-height: 1.6;
  margin: 0;
}

/* Offers Section */
.offers-section {
  padding: 0;
  background: var(--light-gray);
  position: relative;
  width: 100%;
  margin: 0;
  scroll-margin-top: 80px;
}

.offers-section .container {
  position: relative;
  z-index: 2;
  padding: 5rem 2rem;
}

.offers-section h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--black);
}

/* Carousel Arrows - Hidden on Desktop */
.offers-carousel-container {
  position: relative;
  width: 100%;
}

.carousel-arrow {
  display: none;
}

/* Filter Buttons */
.offers-filter {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin: 2rem 0 3rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.8rem 1.8rem;
  border: 2px solid var(--primary-blue);
  background: var(--white);
  color: var(--secondary-blue);
  border-radius: var(--border-radius-lg);
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  position: relative;
  overflow: hidden;
}

.filter-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--gradient-primary);
  transition: left 0.3s ease;
  z-index: -1;
}

.filter-btn:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
  color: var(--white);
  border-color: var(--secondary-blue);
}

.filter-btn:hover::before {
  left: 0;
}

.filter-btn.active {
  background: var(--gradient-primary);
  color: var(--white);
  border-color: var(--secondary-blue);
  box-shadow: var(--shadow-md);
  transform: translateY(-3px);
}

.offers-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
  margin-top: 3rem;
}

@media (min-width: 768px) {
  .offers-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

.offer-card {
  background: var(--white);
  border-radius: var(--border-radius-lg);
  padding: 2rem;
  box-shadow: var(--shadow-md);
  transition: all 0.4s ease;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  border: 2px solid transparent;
}

.offer-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--gradient-primary);
}

.offer-card:hover {
  transform: translateY(-10px);
  box-shadow: var(--shadow-lg);
  border-color: var(--primary-blue);
}

.offer-card.featured {
  border-color: var(--secondary-blue);
  transform: scale(1.02);
}

.offer-card.featured:hover {
  transform: scale(1.05) translateY(-10px);
}

.offer-badge-featured {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: var(--gradient-primary);
  color: var(--white);
  padding: 0.4rem 1rem;
  border-radius: 20px;
  font-weight: 600;
  font-size: 0.9rem;
  z-index: 10;
}

.offer-header {
  margin-bottom: 1.5rem;
}

.offer-header h3 {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.offer-badge {
  display: inline-block;
  background: var(--light-blue);
  color: var(--secondary-blue);
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: 500;
}

.offer-description {
  margin-bottom: 1.5rem;
}

.offer-intro {
  color: var(--medium-gray);
  line-height: 1.6;
  font-size: 1rem;
}

.offer-features {
  flex: 1;
  margin-bottom: 1.5rem;
}

.feature-item {
  display: flex;
  align-items: flex-start;
  gap: 0.8rem;
  margin-bottom: 1rem;
  padding: 0.5rem;
  border-radius: 8px;
  transition: all 0.3s ease;
}

.feature-item:hover {
  background: var(--light-blue);
}

.feature-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
}

.feature-item span:last-child {
  color: var(--dark-gray);
  line-height: 1.5;
  font-size: 0.95rem;
}

.offer-footer {
  margin-top: auto;
  padding-top: 1.5rem;
  border-top: 2px solid var(--light-gray);
}

.offer-meta {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.meta-item {
  color: var(--medium-gray);
  font-size: 0.9rem;
}

.meta-item strong {
  color: var(--black);
  margin-right: 0.3rem;
}

.offers-cta {
  text-align: center;
  margin-top: 3rem;
}

.offers-cta .btn {
  font-size: 1.1rem;
  padding: 1.2rem 2.5rem;
  border: 2px solid var(--primary-blue);
  background: var(--white);
  color: var(--secondary-blue);
  position: relative;
  overflow: hidden;
}

.offers-cta .btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--gradient-primary);
  transition: left 0.3s ease;
  z-index: -1;
}

.offers-cta .btn:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-md);
  color: var(--white);
  border-color: var(--secondary-blue);
}

.offers-cta .btn:hover::before {
  left: 0;
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
  background: var(--light-blue);
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
  color: var(--black);
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
  color: var(--black);
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
  border-color: var(--primary-blue);
}

.form-group textarea {
  resize: vertical;
  min-height: 100px;
}

.submit-btn {
  background: var(--secondary-blue);
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
  background: var(--dark-blue);
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

.faq-accordion {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 900px;
  margin: 0 auto;
}

.faq-item {
  background: white;
  border-radius: 12px;
  border: 2px solid var(--light-gray);
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
}

.faq-item:hover {
  border-color: var(--primary-blue);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

.faq-item.open {
  border-color: var(--secondary-blue);
  box-shadow: 0 4px 16px rgba(99, 102, 241, 0.2);
}

.faq-question {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem 1.5rem;
  background: white;
  transition: background 0.3s ease;
}

.faq-item:hover .faq-question {
  background: var(--light-gray);
}

.faq-item.open .faq-question {
  background: var(--gradient-secondary);
}

.faq-question h5 {
  font-size: 1.1rem;
  margin: 0;
  color: var(--black);
  font-weight: 600;
  flex: 1;
  padding-right: 1rem;
}

.faq-icon {
  font-size: 1.5rem;
  font-weight: 300;
  color: var(--secondary-blue);
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--light-blue);
  border-radius: 50%;
  flex-shrink: 0;
  transition: all 0.3s ease;
}

.faq-item.open .faq-icon {
  background: var(--secondary-blue);
  color: white;
  transform: rotate(180deg);
}

.faq-answer {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s ease, padding 0.4s ease;
  padding: 0 1.5rem;
}

.faq-item.open .faq-answer {
  max-height: 500px;
  padding: 0 1.5rem 1.5rem 1.5rem;
}

.faq-answer p {
  color: var(--medium-gray);
  line-height: 1.7;
  margin: 0;
  font-size: 1rem;
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
    radial-gradient(circle at 30% 20%, rgba(255,255,255,0.15) 0%, transparent 50%),
    radial-gradient(circle at 70% 80%, rgba(182, 216, 242, 0.2) 0%, transparent 50%);
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

.final-cta .btn-primary {
  border: 2px solid var(--white);
  background: var(--white);
  color: var(--secondary-blue);
  position: relative;
  overflow: hidden;
}

.final-cta .btn-primary::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(255,255,255,0.2) 0%, rgba(255,255,255,0.1) 100%);
  transition: left 0.3s ease;
  z-index: -1;
}

.final-cta .btn-primary:hover {
  background: transparent;
  color: var(--white);
  border-color: var(--white);
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(0,0,0,0.2);
}

.final-cta .btn-primary:hover::before {
  left: 0;
}

@media (max-width: 768px) {
  .hero {
    padding: 4rem 1rem 3rem;
    text-align: center;
    justify-content: center;
  }

  .hero-video {
    display: none;
  }

  .hero-background {
    background: var(--gradient-primary);
  }

  .hero-content {
    padding-left: 0;
    margin: 0 auto;
    max-width: 800px;
  }

  .hero-layout {
    flex-direction: column;
    text-align: center;
    gap: 2rem;
  }

  .hero-text {
    max-width: 100%;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-slogan {
    font-size: 1.3rem;
  }

  .hero-description {
    display: none;
  }

  .hero-actions {
    align-items: center;
    width: 100%;
  }

  .hero-particles {
    display: none;
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

  .values-grid {
    grid-template-columns: 1fr;
  }

  .value-card {
    padding: 1.5rem 1rem;
  }

  /* Réduction des tailles de texte */
  .about-section h2,
  .services-section h2,
  .contact-section h2,
  .faq-section h2 {
    font-size: 2rem;
  }

  .value-card h4,
  .service-item h4 {
    font-size: 1.2rem;
  }

  .value-card p,
  .service-item p,
  .story-text p,
  .section-subtitle {
    font-size: 0.95rem;
  }

  .value-icon {
    font-size: 2.5rem;
    margin-bottom: 0.5rem;
  }

  .faq-question h5 {
    font-size: 1rem;
  }

  .faq-answer p {
    font-size: 0.95rem;
  }

  .faq-icon {
    width: 28px;
    height: 28px;
    font-size: 1.3rem;
  }

  /* Testimonials Section Mobile */
  .testimonials-section .container {
    padding: 3rem 1rem;
  }

  .testimonials-section h2 {
    font-size: 2rem;
  }

  .testimonial-content {
    padding: 2rem;
  }

  .testimonial-content p {
    font-size: 1rem;
  }

  .author-avatar {
    width: 50px;
    height: 50px;
    font-size: 2.5rem;
  }

  .author-info h5 {
    font-size: 1rem;
  }

  .author-info span {
    font-size: 0.8rem;
  }

  /* Trusted Brands Section Mobile */
  .trusted-brands-section .container {
    padding: 3rem 1rem;
  }

  .trusted-brands-section h2 {
    font-size: 2rem;
  }

  .brand-logo {
    flex: 0 0 150px;
    height: 100px;
  }

  .logo-placeholder {
    padding: 1rem;
  }

  .logo-placeholder span {
    font-size: 1.5rem;
  }

  .logo-placeholder h4 {
    font-size: 0.8rem;
  }

  /* Services Section Mobile */
  .services-grid {
    grid-template-columns: 1fr;
  }

  /* Offers Section Mobile */
  .offers-section .container {
    padding: 3rem 1rem;
  }

  .offers-section h2 {
    font-size: 2rem;
  }

  .offers-filter {
    flex-direction: row;
    gap: 0.8rem;
    margin: 1.5rem 0 2rem;
    overflow-x: auto;
    overflow-y: hidden;
    justify-content: flex-start;
    padding: 0.5rem 0;
    scroll-behavior: smooth;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: thin;
    scrollbar-color: var(--primary-blue) var(--light-gray);
  }

  .offers-filter::-webkit-scrollbar {
    height: 4px;
  }

  .offers-filter::-webkit-scrollbar-track {
    background: var(--light-gray);
    border-radius: 10px;
  }

  .offers-filter::-webkit-scrollbar-thumb {
    background: var(--primary-blue);
    border-radius: 10px;
  }

  .filter-btn {
    flex-shrink: 0;
    white-space: nowrap;
    padding: 0.8rem 1.5rem;
    font-size: 0.95rem;
  }

  .offers-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .offer-card {
    padding: 1rem;
  }

  .offer-card.featured {
    transform: scale(1);
  }

  .offer-header {
    margin-bottom: 1rem;
  }

  .offer-header h3 {
    font-size: 1.4rem;
    margin-bottom: 0.3rem;
  }

  .offer-description {
    margin-bottom: 1.2rem;
  }

  .offer-intro {
    font-size: 0.9rem;
    line-height: 1.5;
  }

  .offer-features {
    margin-bottom: 1.2rem;
  }

  .feature-item {
    gap: 0.5rem;
    margin-bottom: 0.5rem;
    padding: 0.25rem;
  }

  .feature-item span:last-child {
    font-size: 0.85rem;
    line-height: 1.4;
  }

  .feature-icon {
    font-size: 1rem;
  }

  .offer-footer {
    padding-top: 1rem;
  }

  .offer-meta {
    gap: 0.5rem;
  }

  .meta-item {
    font-size: 0.85rem;
  }

  .offers-cta .btn {
    width: 100%;
    max-width: 300px;
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

  .faq-accordion {
    gap: 0.8rem;
  }

  .faq-question {
    padding: 1rem 1.2rem;
  }

  .faq-item.open .faq-answer {
    padding: 0 1.2rem 1.2rem 1.2rem;
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
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .hero-slogan {
    font-size: 1.1rem;
    margin-bottom: 1.5rem;
  }

  .hero-description {
    font-size: 1rem;
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
  .service-item h4 {
    font-size: 1.1rem;
  }

  .value-card p,
  .service-item p,
  .story-text p,
  .section-subtitle {
    font-size: 0.85rem;
  }

  .faq-question h5 {
    font-size: 0.95rem;
  }

  .faq-answer p {
    font-size: 0.85rem;
  }

  .faq-icon {
    width: 26px;
    height: 26px;
    font-size: 1.2rem;
  }

  .faq-question {
    padding: 0.9rem 1rem;
  }

  .faq-item.open .faq-answer {
    padding: 0 1rem 1rem 1rem;
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

  /* Testimonials Section Very Small Mobile */
  .testimonials-section .container {
    padding: 2rem 1rem;
  }

  .testimonials-section h2 {
    font-size: 1.8rem;
  }

  .testimonial-content {
    padding: 1.5rem;
  }

  .testimonial-content p {
    font-size: 0.9rem;
  }

  .stars {
    font-size: 1.2rem;
  }

  .author-avatar {
    width: 45px;
    height: 45px;
    font-size: 2rem;
  }

  .author-info h5 {
    font-size: 0.9rem;
  }

  .author-info span {
    font-size: 0.75rem;
  }

  /* Trusted Brands Section Very Small Mobile */
  .trusted-brands-section .container {
    padding: 2rem 1rem;
  }

  .trusted-brands-section h2 {
    font-size: 1.8rem;
  }

  .brand-logo {
    flex: 0 0 120px;
    height: 80px;
  }

  .logo-placeholder {
    padding: 0.8rem;
  }

  .logo-placeholder span {
    font-size: 1.2rem;
  }

  .logo-placeholder h4 {
    font-size: 0.7rem;
  }

  /* Offers Section Very Small Mobile */
  .offers-section .container {
    padding: 2rem 1rem;
  }

  .offers-section h2 {
    font-size: 1.8rem;
  }

  .offers-filter {
    gap: 0.6rem;
    margin: 1rem 0 1.5rem;
    padding: 0.3rem 0;
  }

  .filter-btn {
    padding: 0.7rem 1.2rem;
    font-size: 0.85rem;
  }

  .carousel-arrow {
    width: 35px;
    height: 35px;
    font-size: 1.8rem;
    line-height: 1;
  }

  .carousel-arrow-left {
    left: -5px;
  }

  .carousel-arrow-right {
    right: -5px;
  }

  .offers-grid {
    gap: 1rem;
    padding: 0.8rem 0;
  }

  .offer-card {
    padding: 0.8rem;
    min-width: calc(100% - 30px);
    max-width: calc(100% - 30px);
    margin: 0 15px;
  }

  .offer-header {
    margin-bottom: 0.8rem;
  }

  .offer-header h3 {
    font-size: 1.2rem;
    margin-bottom: 0.2rem;
  }

  .offer-badge {
    font-size: 0.7rem;
    padding: 0.2rem 0.5rem;
  }

  .offer-badge-featured {
    font-size: 0.75rem;
    padding: 0.25rem 0.7rem;
  }

  .offer-description {
    margin-bottom: 1rem;
  }

  .offer-intro {
    font-size: 0.85rem;
    line-height: 1.4;
  }

  .offer-features {
    margin-bottom: 0.8rem;
  }

  .feature-item {
    margin-bottom: 0.6rem;
    padding: 0.2rem;
    gap: 0.4rem;
  }

  .feature-item span:last-child {
    font-size: 0.8rem;
    line-height: 1.35;
  }

  .feature-icon {
    font-size: 0.9rem;
  }

  .offer-footer {
    padding-top: 0.8rem;
  }

  .offer-meta {
    gap: 0.4rem;
  }

  .meta-item {
    font-size: 0.8rem;
  }
}
</style>
