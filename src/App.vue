<template>
  <TheNavbar></TheNavbar>
  <SearchInp></SearchInp>
  <Table_Operadoras></Table_Operadoras>
  
</template>

<script>
import TheNavbar from './components/TheNavbar.vue'
import SearchInp from './components/SearchInp.vue';
import Table_Operadoras from './components/Table_Operadoras.vue';

export default {
  name: 'App',
  components: {
    TheNavbar,
    SearchInp,
    Table_Operadoras
  }
}
</script>

<style>

:root {
  --charcoal: #304255ff;
  --charcoal-2: #35495eff;
  --mint: #42b883ff;
  --mint-2: #a6dec5;
  --mint-cream: #f0f9f5ff;
  --input-bg-color: #F8F9FA;
}

body{
  background-color: var(--mint-cream);
}

#app {
  font-family: "Varela Round", sans-serif;
  font-weight: 600;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--charcoal);
  background-color: var(--mint-cream);
}
</style>
