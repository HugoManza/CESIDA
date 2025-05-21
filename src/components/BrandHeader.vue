<template>
  <header class="header" :class="{ 'landing-mode': !isHeaderMode, 'header-mode': isHeaderMode }">
    <div class="landing-content">
      <div class="landing-text">
        <div class="landing-logo">CESIDA</div>
        <h1>Br<span class="script">a</span>nd Ma<span class="script">n</span>ua<span class="script">l</span></h1>
        <p>Alejandra Veloso <br>Hugo Manzano <br>Ana Díaz</p>
      </div>
      <div class="landing-image">
        <div class="image-container">
          <img src="../assets/img/Pictogramas2.png" alt="CESIDA Brand Illustration" class="hero-image">
        </div>
      </div>
    </div>
    <div class="header-content">
      <div class="header-logo"><img src="/src/assets/img/logos/CESIDA_White.svg" alt=""></div>
      <div class="header-title">Manual de Marca</div>
    </div>
  </header>
</template>

<script setup>

</script>

<style scoped></style>