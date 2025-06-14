<template>
  <div class="page">
    <header class="banner">
      <h1>Tags</h1>
    </header>

    <main class="gallery">
      <ImageCard
        v-for="(img, index) in images"
        :key="index"
        :src="img.src"
        @click="openModal(img.src)"
      />
    </main>

    <!-- Modal -->
    <div v-if="selectedImage" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <button class="close-btn" @click="closeModal">✕</button>
        <img :src="selectedImage" alt="Full view" />
      </div>
    </div>

    <!-- Back to Top Button -->
    <button
      class="back-to-top"
      @click="scrollToTop"
      v-show="showScrollTop"
    >
      ↑
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import ImageCard from './components/ImageCard.vue'

const selectedImage = ref(null)
const showScrollTop = ref(false)

const images = [
  { src: '/Graffiti-Showcase/tags/tag1G.jpg' },
  { src: '/Graffiti-Showcase/tags/tag1GJ.jpg' },
  { src: '/Graffiti-Showcase/tags/tag1J.jpg' },
  { src: '/Graffiti-Showcase/tags/tag2G.jpg' },
  { src: '/Graffiti-Showcase/tags/tag2GJ.jpg' },
  { src: '/Graffiti-Showcase/tags/tag2J.jpg' },
  { src: '/Graffiti-Showcase/tags/tag3J.jpg' },
  { src: '/Graffiti-Showcase/tags/tag4J.jpg' },
  { src: '/Graffiti-Showcase/tags/tag5J.jpg' },
]

const openModal = (src) => {
  selectedImage.value = src
}

const closeModal = () => {
  selectedImage.value = null
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

// Show button only when scrolled down
const handleScroll = () => {
  showScrollTop.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.banner {
  position: sticky;
  top: 0;
  background: linear-gradient(90deg, #e60073, #9c27b0);
  color: white;
  text-align: center;
  padding: 1.5rem 0;
  font-size: 1.8rem;
  font-weight: bold;
  z-index: 10;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
  padding: 1rem;
}

/* Modal */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.85);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 50;
}

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 90vh;
}

.modal-content img {
  max-width: 100%;
  max-height: 100%;
  border-radius: 10px;
  box-shadow: 0 0 15px black;
}

.close-btn {
  position: absolute;
  top: -15px;
  right: -15px;
  background: white;
  border: none;
  border-radius: 50%;
  padding: 0.5rem 0.7rem;
  font-size: 1.2rem;
  cursor: pointer;
  color: black;
}

/* Back to top arrow */
.back-to-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: #e60073;
  border: none;
  color: white;
  font-size: 1.5rem;
  padding: 0.6rem 1rem;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 0 10px #000;
  z-index: 100;
  transition: transform 0.2s ease;
}

.back-to-top:hover {
  transform: scale(1.15);
}
</style>
