<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <div class="img-container">
      <img src="https://image.tmdb.org/t/p/original/1FYAbw0ENueTOEl6YRbl7gdEnUa.png" />
    </div>
    <TheWelcome />
  </main>
</template>

<style scoped>
/* GIF-et tartalmazó konténer stílusai */
.img-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
  /* A teljes képernyő magassága */
}

/* GIF méretének és elhelyezésének beállítása */
.img-container img {
  max-width: 100%;
  /* Az ablak méretéhez igazodó szélesség */
  height: auto;
}
</style>
