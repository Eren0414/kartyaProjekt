<script>
import { RouterLink, RouterView } from "vue-router";
import { computed } from "vue";

export default {
  provide() {
    return {
      keresoSzo: computed(() => this.keresoSzo),
    };
  },
  watch: {
    searchWordInput(data){
      if (!data) {
        this.keresoSzo = null;
      }
    }
  },
  data() {
    return {
      keresoSzo: null,
      keresoSzoInput: null,
    };
  },
};
</script>

<template>
  <header>
    <div class="container-fluid my-border my-container">
      <h1>Kártya Projekt</h1>

      <nav
        class="my-border p-4 d-flex justify-content-between align-items-center"
      >
        <div>
          <RouterLink to="/">Home</RouterLink> |
          <RouterLink to="/tablazat">Táblázat</RouterLink> |
          <RouterLink to="/kartyak">Kártyák</RouterLink>
        </div>

        <div class="d-flex align-items-center" role="search">
        <label for="keresoSzo" class="form-label text-nowrap m-0"
          >Kereső:
        </label>
        <input
          id="keresoSzo"
          class="form-control me-2 ms-2"
          type="search"
          aria-label="Keresés"
          v-model="keresoSzoInput"
        />
        <button class="btn btn-outline-success" type="submit"
          @click="keresoSzo = keresoSzoInput"
        >Keresés</button>
      </div>
      </nav>
    </div>
  </header>

  <div class="my-border p-2">
    <RouterView />
  </div>
</template>

<style scoped>
</style>
