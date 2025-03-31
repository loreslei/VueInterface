<template>
  <div class="d-flex justify-content-center container">
    <table class="table mt-5 w-75 border rounded">
      <thead>
        <tr>
          <th v-for="header in tableHeaders" :key="header">{{ header }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in displayedItems" :key="item.registro_ans">
          <td v-for="header in tableHeaders" :key="header">{{ item[header] }}</td>
        </tr>
      </tbody>
    </table>

    <button v-if="displayedItems.length < items.length" @click="loadMoreItems" class="btn btn-primary mt-3">
      Mostrar Mais
    </button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items: [],
      displayedItems: [],
      itemsPerPage: 10,
      tableHeaders: [],
      offset: 0, // Adicionamos um offset para controlar o carregamento dos dados
    };
  },
  methods: {
    fetchData() {
      axios.get(`https://web-production-30e30.up.railway.app/operadoras?offset=${this.offset}&limit=${this.itemsPerPage}`)
        .then(response => {
          if (response.data.length > 0) {
            this.items.push(...response.data); // Adiciona os novos dados ao array items
            this.displayedItems.push(...response.data); // Adiciona os novos dados ao array displayedItems
            if (this.tableHeaders.length === 0) {
              this.tableHeaders = Object.keys(response.data[0]); // Define os cabeçalhos da tabela na primeira chamada
            }
            this.offset += this.itemsPerPage; // Atualiza o offset para a próxima chamada
          }
        })
        .catch(error => {
          console.error('Erro ao buscar dados:', error);
        });
    },
    loadMoreItems() {
      this.fetchData(); // Carrega mais 10 itens
    },
  },
  mounted() {
    this.fetchData(); // Carrega os primeiros 10 itens
  },
};
</script>

<style>
.table {
  align-self: center;
  overflow-x: auto;
}

.container {
  flex-direction: column;
}

th,
td {
  color: var(--charcoal-2) !important;
}
</style>