<template>
  <TheNavbar></TheNavbar>
  <h1 class="mt-5 header-text">Busca de Operadoras <i class="fa-regular fa-building mx-3"></i></h1>
  <SearchInp @search="handleSearch" />
  <Table_Operadoras :searchQuery="searchQuery" />
  <footer class="mt-3 mb-3">© Lorenna Aguiar Nunes</footer>
</template>

<script>
import TheNavbar from './components/TheNavbar.vue';
import SearchInp from './components/SearchInp.vue';
import Table_Operadoras from './components/Table_Operadoras.vue';

export default {
  name: 'App',
  components: {
    TheNavbar,
    SearchInp,
    Table_Operadoras,
  },
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    handleSearch(query) {
      this.searchQuery = query;
    },
  },
};
</script>

<style>
:root {
  --charcoal: #304255ff;
  --charcoal-2: #35495eff;
  --mint: #42b883ff;
  --mint-2: #a6dec5;
  --mint-cream: #f0f9f5ff;
  --input-bg-color: #f8f9fa;
}

body {
  background-color: var(--mint-cream);
  width: 100vw;
  height: 100vh;
}

#app {
  font-family: 'Varela Round', sans-serif;
  font-weight: 600;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--charcoal);
  background-color: var(--mint-cream);
}
</style>