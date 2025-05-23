<template>
  <div class="carousel-container">
    <!-- Versión Desktop -->
    <div class="desktop-carousel" v-if="!isMobile">
      <button class="nav-button left" @click="prevImage" aria-label="Previous image">
        &lt;
      </button>
      
      <div class="image-container">
        <img 
          v-for="(img, index) in images" 
          :key="index" 
          :src="img" 
          :alt="'Image ' + (index + 1)"
          :class="{ 'active': currentIndex === index }"
        />
      </div>
      
      <button class="nav-button right" @click="nextImage" aria-label="Next image">
        &gt;
      </button>
    </div>
    
    <!-- Versión Móvil -->
    <div class="mobile-carousel" v-else>
      <img 
        v-for="(img, index) in images" 
        :key="index" 
        :src="img" 
        :alt="'Image ' + (index + 1)"
      />
    </div>
  </div>
</template>

<script>
import img1 from '@/assets/1.png';
import img2 from '@/assets/2.png';
import img3 from '@/assets/3.png';
import img4 from '@/assets/4.png';
import img5 from '@/assets/5.png';
import img6 from '@/assets/6.png';
import img7 from '@/assets/7.png';

export default {
  name: 'ImageCarousel',
  data() {
    return {
      images: [img1, img2, img3, img4, img5, img6, img7],
      currentIndex: 0,
      isMobile: false
    }
  },
  methods: {
    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    checkScreenSize() {
      this.isMobile = window.innerWidth <= 768;
    },
    handleKeyDown(e) {
      if (!this.isMobile) {
        if (e.key === 'ArrowRight') this.nextImage();
        if (e.key === 'ArrowLeft') this.prevImage();
      }
    }
  },
  mounted() {
    this.checkScreenSize();
    window.addEventListener('resize', this.checkScreenSize);
    window.addEventListener('keydown', this.handleKeyDown);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.checkScreenSize);
    window.removeEventListener('keydown', this.handleKeyDown);
  }
}
</script>

<style scoped>


.carousel-container {
  width: 100%;
  height: 100%;
}

/* Estilos para Desktop */
.desktop-carousel {
  position: relative;
  width: 100%;
  height: 80vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.image-container {
  width: 80%;
  height: 100%;
  position: relative;
}

.desktop-carousel img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: contain;
  opacity: 0;
  transition: opacity 0.5s ease;
}

.desktop-carousel img.active {
  opacity: 1;
}

.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 15px;
  cursor: pointer;
  font-size: 24px;
  z-index: 10;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-button:hover {
  background: rgba(0, 0, 0, 0.8);
}

.left {
  left: 20px;
}

.right {
  right: 20px;
}

/* Estilos para Móvil */
.mobile-carousel {
  width: 100%;
  height: 100vh;
  overflow-y: auto;
  scroll-snap-type: y mandatory;
}

.mobile-carousel img {
  width: 100%;
  height: 100vh;
  object-fit: contain;
  scroll-snap-align: start;
}

/* Opcional: Ocultar scrollbar en algunos navegadores */
.mobile-carousel::-webkit-scrollbar {
  display: none;
}

.mobile-carousel {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

/* Media queries para responsividad */
@media (max-width: 768px) {
  .desktop-carousel {
    display: none;
  }
}

@media (min-width: 769px) {
  .mobile-carousel {
    display: none;
  }
}

.carousel-container {
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

/* Estilos para Desktop */
.desktop-carousel {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.image-container {
  width: 100%;
  height: 100%;
  position: relative;
}

.desktop-carousel img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover; /* Cambiado de 'contain' a 'cover' para llenar todo el espacio */
  opacity: 0;
  transition: opacity 0.5s ease;
}

.desktop-carousel img.active {
  opacity: 1;
}

.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 15px;
  cursor: pointer;
  font-size: 24px;
  z-index: 10;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Estilos para Móvil */
.mobile-carousel {
  width: 100vw;
  height: 100vh;
  overflow-y: auto;
  scroll-snap-type: y mandatory;
}

.mobile-carousel img {
  width: 100%;
  height: 100vh;
  object-fit: cover; /* Cambiado de 'contain' a 'cover' */
  scroll-snap-align: start;
}
</style>