<template>
  <div class="d-flex justify-content-center container">
    <div class="table-responsive w-75" style="margin: 0 auto;">
      <table class="table mt-5 border rounded">
        <thead>
          <tr>
            <th class="text-uppercase" v-for="header in formattedHeaders" :key="header">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in paginatedItems" :key="item.registro_ans">
            <td
              class="text-truncate text-capitalize"
              v-for="header in formattedHeaders"
              :key="header"
              :title="formatDate(item[originalHeaders[header]])"
            >
              <div style="max-height: 500px; overflow-y: auto;">
                {{ formatDate(item[originalHeaders[header]]) }}
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <nav id="nav-pages" aria-label="Page navigation example">
      <ul class="pagination mt-4">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a class="page-link" href="#" @click.prevent="changePage(currentPage - 1)">Anterior</a>
        </li>
        <li class="page-item" v-for="page in visiblePages" :key="page" :class="{ active: currentPage === page }">
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
  props: {
    searchQuery: String,
  },
  data() {
    return {
      items: [],
      currentPage: 1,
      itemsPerPage: 10,
      tableHeaders: [],
      maxVisiblePages: 5,
      originalHeaders: {},
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
    visiblePages() {
      let startPage = Math.max(1, this.currentPage - Math.floor(this.maxVisiblePages / 2));
      let endPage = Math.min(this.totalPages, startPage + this.maxVisiblePages - 1);

      if (endPage - startPage + 1 < this.maxVisiblePages) {
        startPage = Math.max(1, endPage - this.maxVisiblePages + 1);
      }

      return Array.from({ length: endPage - startPage + 1 }, (_, i) => startPage + i);
    },
    formattedHeaders() {
      return this.tableHeaders.map((header) => header.replace(/_/g, ' '));
    },
  },
  methods: {
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    fetchData() {
      const url = this.searchQuery
        ? `https://web-production-30e30.up.railway.app/operadoras/${this.searchQuery}`
        : 'https://web-production-30e30.up.railway.app/operadoras';

      axios
        .get(url)
        .then((response) => {
          this.items = response.data.map((item) => {
            const newItem = {};
            for (const key in item) {
              if (typeof item[key] === 'string') {
                newItem[key] = item[key].toLowerCase();
              } else {
                newItem[key] = item[key];
              }
            }
            return newItem;
          });
          if (this.items.length > 0) {
            this.tableHeaders = Object.keys(this.items[0]);
            this.tableHeaders.forEach((header) => {
              this.originalHeaders[header.replace(/_/g, ' ')] = header;
            });
          }
        })
        .catch((error) => {
          console.error('Erro ao buscar dados:', error);
        });
    },
    formatDate(dateString) {
      if (!dateString) return '';
      const date = new Date(dateString);
      const day = String(date.getDate()).padStart(2, '0');
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const year = date.getFullYear();
      return `${day}/${month}/${year}`;
    },
  },
  mounted() {
    this.fetchData();
  },
  watch: {
    searchQuery() {
      this.fetchData();
    },
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
  min-width: 150px;
  padding: 8px;
  white-space: nowrap;
}

body {
  font-family: 'Varela Round', sans-serif;
}

/* Estilos da Barra de Rolagem */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #555;
}

/* Estilos da Barra de Rolagem para Firefox */
html {
  scrollbar-width: thin;
  scrollbar-color: #888 #f1f1f1;
}
</style>