<template>
  <div class="main-page">
    <!-- Header Component -->
    <BrandHeader :currentSection="currentSection" :isHeaderMode="isHeaderMode" />


    <!-- Main Content Component -->
    <main class="main-content" id="mainContent">
      <BrandSection v-for="section in sections" :key="section.id" :section="section"
        :isActive="currentSection === section.id" :exitDirection="exitDirection" />
    </main>

    <!-- Theme Indicator Component -->
   
    <!-- Section Transition Effect -->
    <div class="section-transition"
      :class="{ 'active': isTransitioning, [`slide-${transitionDirection}`]: transitionDirection }"></div>
  </div>
</template>

<!-- <Hellloooo -->





<style>




@media (max-width: 768px) {
  .main-content {
    padding: .5rem;
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
  }
}
</style>

<script setup>
import { ref, computed, watch, onMounted } from 'vue'
import BrandHeader from './components/BrandHeader.vue'



// Sections data
const sections = [
  { id: 'logos', title: 'Logos', content: 'logos' },
  { id: 'Tipografía', title: 'Tipografía', content: 'Tipografía' },
  { id: 'colors', title: 'Colores', content: 'colors' },
  { id: 'icons', title: 'Iconos', content: 'icons' },
  { id: 'images', title: 'Visuales', content: 'images' }
]

// State
const currentSection = ref('logos')
const isHeaderMode = ref(false)
const isIndicatorVisible = ref(false)
const isTransitioning = ref(false)
const transitionDirection = ref(null)
const exitDirection = ref(null)

// Computed properties
const currentSectionName = computed(() => {
  const section = sections.find(s => s.id === currentSection.value)
  return section ? section.title : ''
})

// Change section function
const changeSection = (sectionId) => {
  // Get section index
  const currentIndex = sections.findIndex(s => s.id === currentSection.value)
  const newIndex = sections.findIndex(s => s.id === sectionId)

  if (newIndex === -1) return

  // Determine direction for animation
  const direction = newIndex > currentIndex ? 'right' : 'left'
  transitionDirection.value = direction
  exitDirection.value = direction === 'right' ? 'left' : 'right'

  // Show transition effect
  showTransitionEffect()

  // Update current section after a short delay
  setTimeout(() => {
    currentSection.value = sectionId
    document.body.className = `theme-${sectionId}`
    showThemeIndicator()
  }, 100)
}

// Show theme indicator
const showThemeIndicator = () => {
  isIndicatorVisible.value = true
  setTimeout(() => {
    isIndicatorVisible.value = false
  }, 2000)
}

// Show transition effect
const showTransitionEffect = () => {
  isTransitioning.value = true
  setTimeout(() => {
    isTransitioning.value = false
  }, 500)
}

// Handle scroll for sticky header effect
const handleScroll = () => {
  isHeaderMode.value = window.scrollY > .1
}

// Lifecycle hooks
onMounted(() => {
  // Initialize with the first theme
  document.body.classList.add(`theme-${currentSection.value}`)

  // Add scroll event listener
  window.addEventListener('scroll', handleScroll)

  // Clean up on unmount
  return () => {
    window.removeEventListener('scroll', handleScroll)
  }
})
</script>