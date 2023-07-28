<template>
  <div class="table-responsive container">
    <table class="table table-striped table-hover">
      <caption>
        List of Units
      </caption>
      <thead>
        <tr>
          <th scope="col" id="code-header">Code</th>
          <th scope="col" id="desc-header">Description</th>
          <th scope="col" id="cp-header">CP</th>
          <th scope="col" id="type-header">Type</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in paginatedData" :key="item.code">
          <td :headers="['code-header']">{{ item.code }}</td>
          <td :headers="['desc-header']">{{ item.desc }}</td>
          <td :headers="['cp-header']">{{ item.cp }}</td>
          <td :headers="['type-header']">{{ item.type }}</td>
        </tr>
      </tbody>
    </table>

    <nav aria-label="Pagination">
      <ul class="pagination">
        <li class="page-item" :class="{ disabled: currentPage === 1 }">
          <a class="page-link" href="#" @click="prevPage">Previous</a>
        </li>
        <li
          class="page-item"
          v-for="page in totalPages"
          :key="page"
          :class="{ active: currentPage === page }"
        >
          <a class="page-link" href="#" @click="goToPage(page)">{{ page }}</a>
        </li>
        <li class="page-item" :class="{ disabled: currentPage === totalPages }">
          <a class="page-link" href="#" @click="nextPage">Next</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UnitSample",
  data() {
    return {
      tableData: [],
      currentPage: 1,
      pageSize: 5,
    };
  },
  async mounted() {
    try {
      const response = await axios.get("./data/data.json");
      this.tableData = response.data;
    } catch (error) {
      console.error("Error fetching data:", error);
    }
  },
  computed: {
    paginatedData() {
      const startIndex = (this.currentPage - 1) * this.pageSize;
      const endIndex = startIndex + this.pageSize;
      return this.tableData.slice(startIndex, endIndex);
    },
    totalPages() {
      return Math.ceil(this.tableData.length / this.pageSize);
    },
  },
  methods: {
    goToPage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
};
</script>
