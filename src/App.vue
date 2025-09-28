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
          <h1 class="logo">Muslim Visibility</h1>
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
  /* Nouvelle palette de couleurs moderne */
  --primary-blue: #4A90E2;
  --light-blue: #E3F2FD;
  --dark-blue: #2171B5;
  --violet: #8B5A9F;
  --light-violet: #F3E8FF;
  --dark-violet: #6B46C1;
  --black: #1A1A1A;
  --dark-gray: #2D3748;
  --medium-gray: #718096;
  --light-gray: #EDF2F7;
  --white: #FFFFFF;
  --gradient-primary: linear-gradient(135deg, var(--primary-blue) 0%, var(--violet) 100%);
  --gradient-secondary: linear-gradient(135deg, var(--light-blue) 0%, var(--light-violet) 100%);
  --shadow-sm: 0 2px 8px rgba(74, 144, 226, 0.1);
  --shadow-md: 0 8px 25px rgba(74, 144, 226, 0.15);
  --shadow-lg: 0 20px 40px rgba(74, 144, 226, 0.2);
  --border-radius: 16px;
  --border-radius-lg: 24px;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Poppins', sans-serif;
  line-height: 1.7;
  color: var(--black);
  background: var(--white);
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
}

.navbar {
  max-width: 100%;
  margin: 0;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand .logo {
  font-size: 1.5rem;
  font-weight: 700;
  background: var(--gradient-primary);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  transition: all 0.3s ease;
}

.nav-brand .logo:hover {
  transform: scale(1.05);
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
  color: var(--primary-blue);
  transform: translateY(-2px);
}

.nav-link:hover::before {
  left: 0;
}

.nav-link.router-link-active {
  color: var(--primary-blue);
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
  display: none;
  position: fixed;
  top: 80px;
  left: 0;
  right: 0;
  background: white;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  z-index: 999;
  padding: 2rem;
  transform: translateY(-100%);
  transition: transform 0.3s ease;
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
  }

  .desktop-menu {
    display: none;
  }

  .mobile-menu-btn {
    display: flex;
  }

  .mobile-menu {
    display: block;
  }

  .nav-brand .logo {
    font-size: 1.2rem;
  }

  .footer-content {
    padding: 0 1rem;
    grid-template-columns: 1fr;
    text-align: center;
  }
}
</style>
