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
    searchWordInput(data) {
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
  computed: {
    isHomePage() {
      return this.$route.path === "/";
    }
  }
};
</script>

<template>
  <header>
    <div class="container-fluid my-border my-container navbar-container">
      <h1 class="navbar-title">Kártya Projekt</h1>

      <nav class="my-border p-4 d-flex justify-content-between align-items-center navbar">
        <div class="navbar-links">
          <RouterLink to="/" class="navbar-link">Home</RouterLink> |
          <RouterLink to="/tablazat" class="navbar-link">Táblázat</RouterLink> |
          <RouterLink to="/kartyak" class="navbar-link">Karakterek</RouterLink>
        </div>

        <div v-if="!isHomePage" class="d-flex align-items-center search-container" role="search">
          <label for="keresoSzo" class="form-label text-nowrap m-0 search-label">Kereső:</label>
          <input id="keresoSzo" class="form-control me-2 ms-2 search-input" type="search" aria-label="Keresés"
            v-model="keresoSzoInput" />
          <button class="btn btn-outline-danger search-button" type="submit"
            @click="keresoSzo = keresoSzoInput">Keresés</button>
        </div>
      </nav>
    </div>
  </header>
  <RouterView />
</template>

<style scope>
body {
  background-color: gray !important;
}

/* Alap navbar konténer */
.navbar-container {
  background-color: #1a1a1a;
  border-bottom: 2px solid #8b0000;
}

/* Cím stílusok */
.navbar-title {
  color: #ff0000;
  font-family: 'Old English Text MT', serif;
  text-shadow: 2px 2px 4px #000;
  text-align: center;
  padding: 15px 0;
  font-size: 2.5rem;
}

/* Navbar stílusok */
.navbar {
  background-color: #1a1a1a;
  padding: 20px;
  border: none;
}

/* Linkek stílusai */
.navbar-links .navbar-link {
  color: #f5f5f5;
  font-family: 'Garamond', serif;
  text-transform: uppercase;
  font-size: 1.2rem;
  text-decoration: none;
  transition: color 0.3s ease;
  position: relative;
  /* Pozicionálás az aláhúzás létrehozásához */
}

.navbar-links .navbar-link:hover {
  color: #ff0000;
  cursor: url('public/cursor.png'), auto;
}

/* Aláhúzás az alábbiakban */
.navbar-links .navbar-link::after {
  content: "";
  /* Üres tartalom az aláhúzáshoz */
  position: absolute;
  /* Pozicionálás */
  left: 0;
  /* Balra igazítva */
  bottom: -5px;
  /* Aláhúzás pozíciója */
  height: 2px;
  /* Aláhúzás vastagsága */
  width: 100%;
  /* Aláhúzás szélessége */
  background-color: #ff0000;
  /* Aláhúzás színe */
  transform: scaleX(0);
  /* Alapértelmezett állapot: nem látható */
  transition: transform 0.3s ease;
  /* Átmenet */
}

.navbar-links .navbar-link:hover::after {
  transform: scaleX(1);
  /* Hover állapotban láthatóvá válik */
}

/* Kereső mező stílusok */
.search-container {
  display: flex;
  align-items: center;
}

.search-label {
  color: #f5f5f5;
  font-size: 1.1rem;
  font-family: 'Garamond', serif;
}

.search-input {
  background-color: #333;
  border: 1px solid #ff0000;
  color: #fff;
  font-family: 'Garamond', serif;
}

.search-button {
  background-color: #8b0000;
  border: 1px solid #ff0000;
  color: #fff;
}

.search-button:hover {
  background-color: #ff0000;
}
</style>
