# Muslim Visibility - Site Vitrine

Site vitrine professionnel pour l'agence Muslim Visibility, spécialisée dans le marketing d'influence éthique.

## 🚀 Fonctionnalités

- **Page unique** : Toutes les sections dans une seule page fluide
- **Section Hero** : Présentation de l'agence avec slogan et call-to-action
- **Section À propos** : Historique, vision, valeurs et présentation de l'équipe
- **Section Contact** : Formulaire de contact et bouton WhatsApp direct
- **Navigation anchor** : Navigation fluide entre les sections avec scroll smooth
- **Design responsive** : Optimisé pour mobile, tablette et desktop
- **Navigation mobile** : Menu hamburger avec animations
- **Design moderne** : Palette de couleurs sophistiquée (bleu clair #4A90E2, violet #8B5A9F, noir #1A1A1A) avec typographie Poppins
- **Animations avancées** : Effets de fade-in, slide-up, hover avec délais progressifs
- **Micro-interactions** : Effets de hover sophistiqués, animations CSS3, particules flottantes
- **Gradients modernes** : Dégradés élégants et ombres portées avec variables CSS

## 🛠️ Technologies utilisées

- **Vue.js 3** avec Composition API
- **TypeScript** pour la robustesse du code
- **Vue Router** pour la navigation
- **CSS3** avec Flexbox et Grid
- **Responsive Design** avec media queries
- **Google Fonts** (Poppins)

## 📋 Installation et lancement

### Prérequis
- Node.js (version 16 ou supérieure)
- npm ou yarn

### Installation
```bash
# Cloner le projet
git clone [repository-url]

# Aller dans le dossier
cd muslim-visibility-site

# Installer les dépendances
npm install
```

### Développement
```bash
# Lancer le serveur de développement
npm run dev

# Le site sera accessible sur http://localhost:5173
```

### Build pour production
```bash
# Créer la version de production
npm run build

# Prévisualiser la version de production
npm run preview
```

### Lint et vérifications
```bash
# Vérifier le code avec ESLint
npm run lint

# Vérification des types TypeScript
npm run type-check
```

## 📱 Responsive Design

Le site est entièrement responsive avec 3 breakpoints principaux :
- **Mobile** : < 768px
- **Tablette** : 768px - 1024px
- **Desktop** : > 1024px

## 🎨 Charte Graphique

### Couleurs principales
- **Bleu principal** : #4A90E2
- **Bleu clair** : #E3F2FD
- **Bleu foncé** : #2171B5
- **Violet** : #8B5A9F
- **Violet clair** : #F3E8FF
- **Violet foncé** : #6B46C1
- **Noir** : #1A1A1A
- **Gris foncé** : #2D3748
- **Gris moyen** : #718096
- **Gris clair** : #EDF2F7
- **Blanc** : #FFFFFF

### Typographie
- **Police** : Poppins (Google Fonts)
- **Poids** : 300, 400, 500, 600, 700

## 📞 Contact WhatsApp

Le bouton WhatsApp est configuré avec le numéro : `+33123456789`

Pour modifier le numéro, recherchez `+33123456789` dans les fichiers et remplacez par le bon numéro.

## 📂 Structure du projet

```
src/
├── components/          # Composants réutilisables
├── views/              # Pages du site
│   └── HomeView.vue    # Page unique avec toutes les sections
├── router/             # Configuration des routes
│   └── index.ts
├── assets/             # Ressources statiques
└── App.vue             # Composant principal avec navigation
```

## 🔧 Personnalisation

### Modifier les informations de contact
- **Email** : Rechercher `contact@muslimvisibility.fr` dans HomeView.vue
- **Téléphone** : Rechercher `+33 1 23 45 67 89` dans HomeView.vue
- **WhatsApp** : Rechercher `+33123456789` dans tous les fichiers

### Modifier les couleurs
Les couleurs principales sont définies dans `App.vue`. Recherchez les codes couleur pour les modifier.

### Ajouter du contenu
- **Textes** : Modifiez directement dans les fichiers Vue
- **Images** : Ajoutez dans le dossier `src/assets/`

## 🚀 Déploiement

Le site peut être déployé sur :
- **Netlify** : Connectez votre repository GitHub
- **Vercel** : Import depuis GitHub
- **Firebase Hosting** : `npm run build` puis `firebase deploy`
- **Serveur classique** : Upload du dossier `dist/` après build

## 📄 Support

Pour toute question ou support, contactez l'équipe de développement.

---

© 2024 Muslim Visibility. Tous droits réservés.
