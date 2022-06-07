<script setup lang="ts">
import GlowBtn from './components/GlowButton/GlowButton.vue'
</script>

<template>
  <div class="container">
    <glow-btn label="Botão 1" variant="primary"/>
    <glow-btn label="Botão 1" variant="secondary"/>
    <glow-btn label="Botão 1" variant="red"/>
    <glow-btn label="Botão 1" variant="#fcf5b7"/>
  </div>
</template>

<style lang="scss">
body {
  background: #27282c;
  .container {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100vh;
    align-items: center;
    justify-content: center;
  }
}

.glow-btn {
  margin-bottom: 40px;
}
</style>
