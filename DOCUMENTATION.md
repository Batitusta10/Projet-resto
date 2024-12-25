# Le Restaurant - Documentation du Projet

## Vue.js 3 - Application de Gestion de Restaurant

Cette application est construite avec Vue.js 3 et utilise les dernières pratiques recommandées, notamment la Composition API avec `<script setup>`.

### 1. Architecture du Projet

L'application est structurée en plusieurs composants et vues :
```
src/
├── components/      # Composants réutilisables
├── views/          # Pages principales
├── router.js       # Configuration des routes
└── main.js         # Point d'entrée
```

### 2. Concepts Vue.js Utilisés

#### Composition API avec `<script setup>`
```vue
<script setup>
import { ref, inject } from 'vue'

const cart = ref([])           // État réactif
const displayToast = inject('displayToast')  // Injection de dépendances
</script>
```

#### State Management avec Provide/Inject
Utilisé pour partager l'état global (panier, commandes) :
```vue
<!-- Dans App.vue -->
<script setup>
import { ref, provide } from 'vue'

const cart = ref([])
provide('cart', cart)
</script>

<!-- Dans un composant enfant -->
<script setup>
import { inject } from 'vue'

const cart = inject('cart')
</script>
```

#### Système de Composants
Exemple de composant réutilisable (DishCard.vue) :
```vue
<script setup>
const props = defineProps({
  dish: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['add-to-cart'])
</script>

<template>
  <div class="card">
    <h3>{{ dish.name }}</h3>
    <button @click="$emit('add-to-cart', dish)">
      Ajouter au panier
    </button>
  </div>
</template>
```

#### Vue Router
Configuration des routes pour la navigation :
```javascript
const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: '/', component: Home },
    { path: '/menu', component: Menu },
    { path: '/cart', component: Cart },
    { path: '/admin', component: Admin }
  ]
})
```

### 3. Fonctionnalités Principales

#### Gestion du Panier
- État réactif avec `ref()`
- Calcul dynamique du total
- Modification des quantités
- Suppression d'articles

#### Système de Notifications
Utilisation d'un composant Toast pour les notifications :
```vue
<template>
  <div class="toast" v-if="showToast">
    {{ message }}
  </div>
</template>
```

#### Gestion des Commandes
- Suivi des commandes en temps réel
- Mise à jour du statut des commandes
- Interface administrateur

### 4. Design et Style

L'application utilise un design minimaliste avec :
- Palette noir et blanc
- Police Roboto
- CSS pur sans framework
- Composants réutilisables stylisés

### 5. Bonnes Pratiques Implémentées

- Composants atomiques et réutilisables
- Séparation des responsabilités
- Props typées
- Gestion d'état centralisée
- Nommage clair et cohérent
- Code commenté et organisé

### 6. Conclusion

Cette application démontre l'utilisation des fonctionnalités modernes de Vue.js 3 tout en maintenant une architecture claire et maintenable. L'utilisation de la Composition API avec `<script setup>` permet un code plus concis et plus facile à maintenir.