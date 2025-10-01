<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue'

const mobileMenuOpen = ref(false)

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value
}

const closeMobileMenu = () => {
  mobileMenuOpen.value = false
}
</script>

<template>
  <div id="app">
    <header class="header">
      <nav class="navbar">
        <div class="nav-brand">
          <img src="/logo.png" alt="Muslim Visibility" class="logo-img">
          <h1 class="logo">MV</h1>
          <span class="logo-full">Muslim Visibility</span>
        </div>

        <!-- Desktop Menu -->
        <div class="nav-menu desktop-menu">
          <a href="#accueil" class="nav-link" @click="closeMobileMenu">Accueil</a>
          <a href="#about" class="nav-link" @click="closeMobileMenu">À propos</a>
          <a href="#contact" class="nav-link" @click="closeMobileMenu">Contact</a>
        </div>

        <!-- Mobile Menu Button -->
        <button class="mobile-menu-btn" @click="toggleMobileMenu" aria-label="Menu">
          <span class="hamburger-line" :class="{ active: mobileMenuOpen }"></span>
          <span class="hamburger-line" :class="{ active: mobileMenuOpen }"></span>
          <span class="hamburger-line" :class="{ active: mobileMenuOpen }"></span>
        </button>

        <!-- Mobile Menu -->
        <div class="mobile-menu" :class="{ active: mobileMenuOpen }">
          <a href="#accueil" class="nav-link-mobile" @click="closeMobileMenu">Accueil</a>
          <a href="#about" class="nav-link-mobile" @click="closeMobileMenu">À propos</a>
          <a href="#contact" class="nav-link-mobile" @click="closeMobileMenu">Contact</a>
        </div>
      </nav>
    </header>

    <main class="main-content">
      <RouterView />
    </main>

    <footer class="footer">
      <div class="footer-content">
        <div class="footer-section">
          <h3>Muslim Visibility</h3>
          <p>Votre agence de marketing d'influence éthique</p>
        </div>
        <div class="footer-section">
          <h4>Suivez-nous</h4>
          <div class="social-links">
            <a href="#" aria-label="Instagram">Instagram</a>
            <a href="#" aria-label="LinkedIn">LinkedIn</a>
            <a href="#" aria-label="Twitter">Twitter</a>
          </div>
        </div>
        <div class="footer-section">
          <a href="#" class="footer-link">Mentions légales</a>
          <a href="#" class="footer-link">Politique de confidentialité</a>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2024 Muslim Visibility. Tous droits réservés.</p>
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  /* Palette moderne bleu ciel personnalisée */
  --primary-blue: #B6D8F2;  /* Bleu ciel principal */
  --secondary-blue: #5784BA; /* Bleu secondaire */
  --light-blue: #E8F2FB;    /* Bleu très clair */
  --dark-blue: #4A6B94;     /* Bleu plus foncé */
  --accent-blue: #3D5F8A;   /* Bleu accent foncé */
  --black: #1a1a1a;         /* Noir profond */
  --dark-gray: #2D3748;     /* Gris foncé */
  --medium-gray: #64748b;   /* Gris moyen */
  --light-gray: #f8fafc;    /* Gris très clair */
  --white: #ffffff;         /* Blanc pur */

  /* Gradients avec nouvelle palette */
  --gradient-primary: linear-gradient(135deg, var(--secondary-blue) 0%, var(--primary-blue) 100%);
  --gradient-secondary: linear-gradient(135deg, var(--light-blue) 0%, var(--white) 100%);
  --gradient-accent: linear-gradient(135deg, var(--dark-blue) 0%, var(--accent-blue) 100%);

  /* Ombres avec teinte bleu personnalisée */
  --shadow-sm: 0 2px 8px rgba(182, 216, 242, 0.15);
  --shadow-md: 0 8px 25px rgba(87, 132, 186, 0.2);
  --shadow-lg: 0 20px 40px rgba(87, 132, 186, 0.25);

  /* Rayons de bordure */
  --border-radius: 16px;
  --border-radius-lg: 24px;
}

html {
  scroll-behavior: smooth;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
  line-height: 1.7;
  color: var(--black);
  background: var(--white);
  margin: 0;
  padding: 0;
}

#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
  width: 100%;
  overflow-x: hidden;
}

.header {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow-sm);
  border-bottom: 1px solid var(--light-gray);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: all 0.3s ease;
  width: 100%;
  margin: 0;
  padding: 0;
}

.navbar {
  max-width: 100%;
  margin: 0;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-shrink: 0;
  position: relative;
  min-width: 250px;
}

.logo-img {
  height: 50px;
  width: auto;
  transition: all 0.3s ease;
  z-index: 1002;
}

.nav-brand .logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--secondary-blue);
  transition: all 0.3s ease;
  position: relative;
  z-index: 1002;
  white-space: nowrap;
}

.logo-full {
  position: absolute;
  left: 60px;
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--secondary-blue);
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
  z-index: 1002;
}

.nav-brand:hover .logo {
  opacity: 0;
}

.nav-brand:hover .logo-full {
  opacity: 1;
}

.nav-menu {
  display: flex;
  gap: 2rem;
}

.nav-link {
  text-decoration: none;
  color: var(--black);
  font-weight: 500;
  padding: 0.5rem 1rem;
  border-radius: var(--border-radius);
  position: relative;
  transition: all 0.3s ease;
  overflow: hidden;
}

.nav-link::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--gradient-secondary);
  transition: left 0.3s ease;
  z-index: -1;
}

.nav-link:hover {
  color: var(--secondary-blue);
  transform: translateY(-2px);
}

.nav-link:hover::before {
  left: 0;
}

.nav-link.router-link-active {
  color: var(--secondary-blue);
  background: var(--light-blue);
}

.mobile-menu-btn {
  display: none;
  flex-direction: column;
  justify-content: space-around;
  width: 30px;
  height: 30px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}

.hamburger-line {
  width: 100%;
  height: 3px;
  background: #333;
  border-radius: 2px;
  transition: all 0.3s ease;
  transform-origin: center;
}

.hamburger-line.active:nth-child(1) {
  transform: rotate(45deg) translateY(9px);
}

.hamburger-line.active:nth-child(2) {
  opacity: 0;
}

.hamburger-line.active:nth-child(3) {
  transform: rotate(-45deg) translateY(-9px);
}

.mobile-menu {
  display: block;
  position: fixed;
  top: 80px;
  left: 0;
  right: 0;
  background: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  z-index: 999;
  padding: 2rem;
  transform: translateY(-200%);
  transition: transform 0.3s ease;
}

@media (min-width: 769px) {
  .mobile-menu {
    display: none;
  }
}

.mobile-menu.active {
  transform: translateY(0);
}

.nav-link-mobile {
  display: block;
  padding: 1rem 0;
  text-decoration: none;
  color: #333;
  font-weight: 500;
  font-size: 1.2rem;
  border-bottom: 1px solid #eee;
  transition: color 0.3s ease;
}

.nav-link-mobile:hover,
.nav-link-mobile.router-link-active {
  color: #2c5aa0;
}

.nav-link-mobile:last-child {
  border-bottom: none;
}

.main-content {
  flex: 1;
  margin-top: 80px;
  width: 100%;
  padding: 0;
  margin-left: 0;
  margin-right: 0;
}

.footer {
  background: var(--white);
  color: var(--black);
  padding: 3rem 0 1rem;
  position: relative;
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: var(--gradient-primary);
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.footer-section h3,
.footer-section h4 {
  margin-bottom: 1rem;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-section p {
  color: var(--medium-gray);
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a,
.footer-link {
  color: var(--medium-gray);
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 0.5rem;
  border-radius: var(--border-radius);
}

.social-links a:hover,
.footer-link:hover {
  color: var(--primary-blue);
  background: rgba(74, 144, 226, 0.1);
  transform: translateY(-2px);
}

.footer-bottom {
  text-align: center;
  padding: 1rem 0;
  border-top: 1px solid var(--medium-gray);
  margin-top: 2rem;
  color: var(--medium-gray);
}

@media (max-width: 768px) {
  .navbar {
    padding: 1rem;
    position: relative;
  }

  .desktop-menu {
    display: none;
  }

  .mobile-menu-btn {
    display: flex;
    z-index: 1001;
  }

  .logo-img {
    height: 40px;
  }

  .nav-brand .logo {
    font-size: 1.2rem;
  }

  .logo-full {
    left: 50px;
    font-size: 1.2rem;
  }

  .mobile-menu {
    top: 70px;
    padding: 1.5rem;
  }

  .nav-link-mobile {
    font-size: 1.1rem;
    padding: 0.8rem 0;
  }

  .main-content {
    margin-top: 70px;
  }

  .footer-content {
    padding: 0 1rem;
    grid-template-columns: 1fr;
    text-align: center;
  }
}

@media (max-width: 480px) {
  .navbar {
    padding: 0.8rem;
  }

  .logo-img {
    height: 35px;
  }

  .nav-brand .logo {
    font-size: 1rem;
  }

  .logo-full {
    left: 45px;
    font-size: 1rem;
  }

  .mobile-menu-btn {
    width: 25px;
    height: 25px;
  }

  .hamburger-line {
    height: 2px;
  }

  .mobile-menu {
    top: 60px;
    padding: 1rem;
  }

  .nav-link-mobile {
    font-size: 1rem;
    padding: 0.6rem 0;
  }

  .main-content {
    margin-top: 60px;
  }
}
</style>
