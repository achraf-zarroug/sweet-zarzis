<script setup lang="ts">
import { ref } from 'vue'

const activeCategory = ref('Tout')
const categories = ['Tout', 'Pâtisseries', 'Gâteaux', 'Gourmandises']
const products = [
  { name: 'Éclat de pistache', type: 'Pâtisseries', note: 'Pistache · vanille · croustillant', image: 'photo-1578985545062-69928b1d9587' },
  { name: 'Douceur du jour', type: 'Gourmandises', note: 'Une petite pause pleine de douceur', image: 'photo-1488477181946-6428a0291777' },
  { name: 'Le gâteau de fête', type: 'Gâteaux', note: 'À partager pour les beaux moments', image: 'photo-1565958011703-44f9829ba187' },
  { name: 'Chou tout chocolat', type: 'Pâtisseries', note: 'Chocolat généreux · cœur fondant', image: 'photo-1551024506-0bccd828d307' },
]
const galleryPhotos = [
  { name: 'Pause glacée', image: '/images/milkshake.jpg', alt: 'Milkshake Sweets tenu à la main' },
  { name: 'Gâteaux à partager', image: '/images/charlotte.jpg', alt: 'Gâteau charlotte décoré d’un ruban violet' },
  { name: 'Gaufre gourmande', image: '/images/waffle.jpg', alt: 'Gaufre garnie de glace et de chocolat' },
]
const visibleProducts = () => activeCategory.value === 'Tout'
  ? products
  : products.filter((product) => product.type === activeCategory.value)
</script>

<template>
  <div class="site-shell">
    <div class="announcement"><span class="announcement-spark">✳</span> Une petite douceur, un grand moment <span class="announcement-spark">✳</span></div>
    <header class="site-header">
      <a class="brand" href="#accueil" aria-label="Sweets Zarzis — accueil">
        <img class="brand-logo" src="/sweets-wordmark.png" alt="Sweets" />
        <span class="brand-name">ZARZIS · PÂTISSERIE</span>
      </a>
      <nav class="main-nav" aria-label="Navigation principale">
        <a href="#maison">À propos</a>
        <a href="#creations">Nos créations</a>
        <a href="#visite">Nous trouver</a>
      </nav>
      <a class="header-cta" href="https://www.instagram.com/sweets_zarzis/" target="_blank" rel="noreferrer">Suivre sur Instagram <span>↗</span></a>
    </header>

    <main>
      <section id="accueil" class="hero">
        <div class="hero-copy">
          <div class="eyebrow"><span class="eyebrow-line"></span> LE GOÛT DES JOLIES CHOSES</div>
          <h1>Un peu de<br /><em>douceur</em> dans<br />chaque jour.</h1>
          <p class="hero-lede">Des créations gourmandes et délicates, imaginées pour savourer les petits et grands moments à Zarzis.</p>
          <div class="hero-actions">
            <a class="button button-dark" href="#creations">Découvrir nos douceurs <span>↓</span></a>
            <a class="text-link" href="#visite">Passer nous voir <span>↗</span></a>
          </div>
          <div class="hero-note"><span class="note-star">✳</span><span>FAIT AVEC AMOUR<br /><strong>À Zarzis, pour vous.</strong></span></div>
        </div>
        <div class="hero-visual">
          <div class="hero-image image-cover" role="img" aria-label="Façade de la pâtisserie Sweets Zarzis, avec son enseigne turquoise et son auvent rayé vert et blanc"></div>
          <div class="image-caption"><span>BIENVENUE CHEZ SWEETS</span><span>01 — 04</span></div>
          <div class="round-stamp"><span class="stamp-top">LA DOUCEUR DE</span><strong>ZARZIS</strong><span class="stamp-bottom">PÂTISSERIE · GLACES</span><span class="stamp-star">✳</span></div>
          <span class="hero-flower flower-one">✿</span><span class="hero-flower flower-two">✳</span>
        </div>
        <div class="hero-bottom"><span>33° 30′ 16.0″ N&nbsp; · &nbsp;11° 06′ 35.2″ E</span><a href="#creations">FAITES DÉFILER <span>↓</span></a></div>
      </section>

      <section id="maison" class="intro-section about-section" aria-labelledby="about-title">
        <div class="about-photo-wrap"><img class="about-photo" src="/images/sweets-boxes-about.jpg" alt="Boîtes vertes Sweets empilées avec le logo de la pâtisserie" loading="lazy" /><span>LES BOÎTES SWEETS · ZARZIS</span></div>
        <div class="about-content"><div class="section-index">01 <span>—</span> À PROPOS</div><h2 id="about-title">La douceur<br />à <em>partager.</em></h2><p>Pâtisseries, glaces et crêpes : Sweets Zarzis vous accueille pour une pause gourmande à partager, sur place ou à emporter.</p><div class="about-signature"><span class="intro-asterisk">✳</span><p>VOTRE MAISON GOURMANDE<br /><strong>Au cœur de Zarzis.</strong></p></div></div>
      </section>

      <section class="gallery-section" aria-labelledby="gallery-title">
        <div class="gallery-heading"><div><div class="section-index">02 <span>—</span> L’UNIVERS SWEETS</div><h2 id="gallery-title">Quelques instants<br /><em>à savourer.</em></h2></div><p>Boissons fraîches, douceurs à partager et petites attentions à emporter : un aperçu de la maison.</p></div>
        <div class="gallery-grid">
          <figure v-for="photo in galleryPhotos" :key="photo.name" class="gallery-card"><img :src="photo.image" :alt="photo.alt" loading="lazy" /><figcaption>{{ photo.name }}</figcaption></figure>
        </div>
      </section>

      <section id="creations" class="creations-section">
        <div class="section-heading">
          <div><div class="section-index">03 <span>—</span> LA VITRINE</div><h2>Nos petites<br /><em>merveilles.</em></h2></div>
          <p>De quoi faire durer le plaisir.<br />Trouvez l’inspiration, puis venez choisir votre douceur préférée en boutique.</p>
        </div>
        <div class="filter-row" aria-label="Filtrer les créations">
          <button v-for="category in categories" :key="category" :class="['filter-chip', { selected: activeCategory === category }]" @click="activeCategory = category">{{ category }}<span v-if="activeCategory === category">↗</span></button>
          <span class="filter-count">{{ String(visibleProducts().length).padStart(2, '0') }} CRÉATIONS</span>
        </div>
        <div class="product-grid">
          <article v-for="(product, index) in visibleProducts()" :key="product.name" class="product-card">
            <div class="product-image image-cover" :style="{ '--photo': `url(https://images.unsplash.com/${product.image}?auto=format&fit=crop&w=900&q=85)` }">
              <span class="product-number">0{{ index + 1 }}</span><span class="product-plus">↗</span>
            </div>
            <div class="product-meta"><div><span class="product-type">{{ product.type }}</span><h3>{{ product.name }}</h3><p>{{ product.note }}</p></div><span class="product-arrow">↗</span></div>
          </article>
        </div>
        <div class="creations-foot"><span>UNE ENVIE PARTICULIÈRE ?</span><a href="https://www.instagram.com/sweets_zarzis/" target="_blank" rel="noreferrer">Écrivez-nous sur Instagram <span>↗</span></a></div>
      </section>

      <section class="quote-section"><span class="quote-ornament">“</span><p>Le bonheur tient parfois<br />dans <em>une bouchée.</em></p><span class="quote-signature">À TRÈS VITE CHEZ SWEETS <span>✳</span></span></section>

      <section id="visite" class="visit-section">
        <div class="visit-info"><div class="section-index">04 <span>—</span> À BIENTÔT ?</div><h2>On vous garde<br />une <em>place.</em></h2><p>Retrouvez-nous à Zarzis et passez découvrir la vitrine. Le plaisir est juste au coin de la rue.</p><a class="button button-light" href="https://www.google.com/maps/dir/?api=1&destination=33.5044197%2C11.1097765" target="_blank" rel="noreferrer">Ouvrir l’itinéraire <span>↗</span></a><a class="visit-instagram" href="https://www.instagram.com/sweets_zarzis/" target="_blank" rel="noreferrer"><span class="instagram-icon">◎</span> @sweets_zarzis</a></div>
        <div class="map-card"><iframe title="Carte de Sweets Zarzis" src="https://maps.google.com/maps?q=33.5044197%2C11.1097765&z=16&output=embed" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe><a class="map-label" href="https://www.google.com/maps/place/Sweets+zarzis/@33.5044197,11.1096156,21z/data=!4m6!3m5!1s0x13aaef0063042929:0xe2c9bef296dda09a!8m2!3d33.5044197!4d11.1097765!16s%2Fg%2F11zxf2vzts" target="_blank" rel="noreferrer"><span class="pin">✳</span><span><strong>Sweets Zarzis</strong><small>Zarzis, Tunisie</small></span><span class="map-arrow">↗</span></a></div>
      </section>
    </main>

    <footer class="site-footer"><a class="brand footer-brand" href="#accueil"><img class="brand-logo" src="/sweets-wordmark.png" alt="Sweets" /><span class="brand-name">ZARZIS · PÂTISSERIE</span></a><span class="footer-note">Une douceur à la fois. <span>✳</span></span><div class="footer-links"><a href="https://www.instagram.com/sweets_zarzis/" target="_blank" rel="noreferrer">INSTAGRAM ↗</a><a href="#accueil">RETOUR EN HAUT ↑</a></div><span class="copyright">© SWEETS ZARZIS</span></footer>
  </div>
</template>




