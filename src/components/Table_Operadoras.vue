<template>
  <div class="d-flex justify-content-center container">
    <div class="table-responsive w-75" style="max-height: 500px; overflow-y: auto;">
      <table class="table mt-5 border rounded">
        <thead>
          <tr>
            <th v-for="header in tableHeaders" :key="header">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in paginatedItems" :key="item.registro_ans">
            <td v-for="header in tableHeaders" :key="header">{{ item[header] }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <nav id="nav-pages" aria-label="Page navigation example">
      <ul class="pagination mt-4">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a class="page-link" href="#" @click.prevent="changePage(currentPage - 1)">Anterior</a>
        </li>
        <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: currentPage === page }">
          <a class="page-link" href="#" @click.prevent="changePage(page)">{{ page }}</a>
        </li>
        <li class="page-item" :class="{ disabled: currentPage === totalPages }">
          <a class="page-link" href="#" @click.prevent="changePage(currentPage + 1)">Próximo</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      items: [],
      currentPage: 1,
      itemsPerPage: 5,
      tableHeaders: [],
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.items.length / this.itemsPerPage);
    },
    paginatedItems() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.items.slice(start, end);
    },
  },
  methods: {
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    fetchData() {
      axios.get('https://web-production-30e30.up.railway.app/operadoras')
        .then(response => {
          this.items = response.data;
          if (this.items.length > 0) {
            this.tableHeaders = Object.keys(this.items[0]);
          }
        })
        .catch(error => {
          console.error('Erro ao buscar dados:', error);
        });
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style>
.nav-pages,
.pagination {
  align-self: center;
  justify-self: center;
}

.container {
  flex-direction: column;
}

th,
td {
  color: var(--charcoal-2) !important;
}
</style>