<template>
  <div class="about">
    <!-- Hero Section -->
    <section class="about-hero">
      <div class="container">
        <h1>À propos de Muslim Visibility</h1>
        <p class="hero-subtitle">L'agence qui révolutionne le marketing d'influence éthique</p>
      </div>
    </section>

    <!-- Notre Histoire -->
    <section class="our-story">
      <div class="container">
        <div class="story-content">
          <div class="story-text">
            <h2>Notre Histoire</h2>
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
              <h3>100+</h3>
              <p>Influenceurs accompagnés</p>
            </div>
            <div class="stat-item">
              <h3>50+</h3>
              <p>Marques partenaires</p>
            </div>
            <div class="stat-item">
              <h3>2M+</h3>
              <p>Portée cumulée</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Notre Vision -->
    <section class="our-vision">
      <div class="container">
        <h2>Notre Vision</h2>
        <p class="vision-text">
          Nous imaginons un monde où le marketing d'influence transcende les stéréotypes
          et crée de véritables connexions humaines. Notre mission est de donner une voix
          authentique à la diversité et de faire du respect mutuel la base de toute collaboration.
        </p>
      </div>
    </section>

    <!-- Nos Valeurs -->
    <section class="our-values">
      <div class="container">
        <h2>Nos Valeurs</h2>
        <div class="values-grid">
          <div class="value-card">
            <div class="value-icon">🤝</div>
            <h3>Éthique</h3>
            <p>
              Nous plaçons l'éthique au cœur de chaque décision, garantissant des
              collaborations respectueuses et alignées avec les valeurs de chacun.
            </p>
          </div>
          <div class="value-card">
            <div class="value-icon">💎</div>
            <h3>Transparence</h3>
            <p>
              La transparence guide toutes nos actions. Pas de surprises, pas de
              malentendus, juste une communication claire et honnête.
            </p>
          </div>
          <div class="value-card">
            <div class="value-icon">❤️</div>
            <h3>Respect</h3>
            <p>
              Le respect mutuel est la base de nos relations. Nous honorons la
              diversité culturelle et les convictions de chaque partenaire.
            </p>
          </div>
          <div class="value-card">
            <div class="value-icon">⭐</div>
            <h3>Excellence</h3>
            <p>
              Nous visons l'excellence dans chaque projet, en offrant un service
              de qualité supérieure et des résultats mesurables.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Notre Équipe (Optionnel) -->
    <section class="our-team">
      <div class="container">
        <h2>Notre Équipe</h2>
        <p class="team-intro">
          Une équipe diverse et expérimentée, unie par la passion de créer des
          collaborations authentiques et impactantes.
        </p>
        <div class="team-grid">
          <div class="team-member">
            <div class="member-avatar">👨‍💼</div>
            <h4>Équipe Direction</h4>
            <p>Vision stratégique et développement</p>
          </div>
          <div class="team-member">
            <div class="member-avatar">👩‍💻</div>
            <h4>Équipe Marketing</h4>
            <p>Créativité et innovation</p>
          </div>
          <div class="team-member">
            <div class="member-avatar">👨‍🤝‍👨</div>
            <h4>Équipe Relations</h4>
            <p>Accompagnement et suivi</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Call to Action -->
    <section class="about-cta">
      <div class="container">
        <h2>Rejoignez l'aventure</h2>
        <p>Que vous soyez influenceur ou entreprise, découvrons ensemble comment créer des collaborations qui ont du sens.</p>
        <div class="cta-buttons">
          <a href="https://wa.me/+33123456789" class="btn btn-primary" target="_blank">
            Contactez-nous
          </a>
          <router-link to="/contact" class="btn btn-secondary">
            Demander un devis
          </router-link>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.about {
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.about-hero {
  background: linear-gradient(135deg, #2c5aa0 0%, #1e3f73 100%);
  color: white;
  padding: 6rem 0 4rem;
  text-align: center;
}

.about-hero h1 {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.hero-subtitle {
  font-size: 1.3rem;
  opacity: 0.9;
}

.our-story {
  padding: 5rem 0;
  background: #f8f9fa;
}

.story-content {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 4rem;
  align-items: center;
}

.story-text h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
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
  gap: 2rem;
}

.stat-item {
  text-align: center;
  padding: 1.5rem;
  background: white;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
}

.stat-item h3 {
  font-size: 2.5rem;
  font-weight: 700;
  color: #2c5aa0;
  margin-bottom: 0.5rem;
}

.stat-item p {
  color: #666;
  font-weight: 500;
}

.our-vision {
  padding: 5rem 0;
  background: white;
  text-align: center;
}

.our-vision h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #333;
}

.vision-text {
  font-size: 1.2rem;
  line-height: 1.7;
  color: #666;
  max-width: 800px;
  margin: 0 auto;
}

.our-values {
  padding: 5rem 0;
  background: #f8f9fa;
}

.our-values h2 {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  color: #333;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.value-card {
  background: white;
  padding: 2.5rem 2rem;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  text-align: center;
  transition: transform 0.3s ease;
}

.value-card:hover {
  transform: translateY(-5px);
}

.value-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.value-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c5aa0;
}

.value-card p {
  color: #666;
  line-height: 1.6;
}

.our-team {
  padding: 5rem 0;
  background: white;
}

.our-team h2 {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 1rem;
  color: #333;
}

.team-intro {
  text-align: center;
  font-size: 1.1rem;
  color: #666;
  margin-bottom: 3rem;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.team-member {
  text-align: center;
  padding: 2rem;
  background: #f8f9fa;
  border-radius: 15px;
  transition: transform 0.3s ease;
}

.team-member:hover {
  transform: translateY(-5px);
}

.member-avatar {
  font-size: 4rem;
  margin-bottom: 1rem;
}

.team-member h4 {
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
  color: #333;
}

.team-member p {
  color: #666;
}

.about-cta {
  background: #333;
  color: white;
  padding: 5rem 0;
  text-align: center;
}

.about-cta h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.about-cta p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.cta-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  display: inline-block;
  padding: 1rem 2rem;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
}

.btn-primary {
  background: #2c5aa0;
  color: white;
}

.btn-primary:hover {
  background: #1e3f73;
  transform: translateY(-2px);
}

.btn-secondary {
  background: white;
  color: #2c5aa0;
}

.btn-secondary:hover {
  background: #f8f9fa;
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .about-hero h1 {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1.1rem;
  }

  .story-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .story-stats {
    flex-direction: row;
    justify-content: space-around;
  }

  .values-grid,
  .team-grid {
    grid-template-columns: 1fr;
  }

  .container {
    padding: 0 1rem;
  }

  .btn {
    width: 100%;
    max-width: 250px;
  }
}
</style>
