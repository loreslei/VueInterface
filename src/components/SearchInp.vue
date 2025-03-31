<template>
    <form class="container-fluid d-flex justify-content-center mt-5" role="search" @submit.prevent="handleSearch">
      <div class="input-group w-50">
        <button class="input-group-text" id="basic-addon1" type="submit">
          <i class="fa-solid fa-magnifying-glass text-muted"></i>
        </button>
        <input
          class="form-control me-2 bg-white"
          type="search"
          placeholder="Buscar Cadastros de Operadoras"
          aria-label="Buscar Cadastros de Operadoras"
          aria-describedby="basic-addon1"
          v-model="searchQuery"
        />
      </div>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: '',
      };
    },
    methods: {
      handleSearch() {
        this.$emit('search', this.searchQuery);
      },
    },
  };
  </script>
  
  <style>
  input.bg-white {
    background-color: var(--input-bg-color) !important;
  }
  
  button,
  input {
    padding: 0.9rem !important;
  }
  
  button {
    padding: 0.9rem 1.5rem !important;
  }
  </style>