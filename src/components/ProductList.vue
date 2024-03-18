<!-- ProductList.vue -->
<template>
    <div class="product-list row">
      <div v-for="product in paginatedProducts" :key="product.id" class="product col-lg-4 col-md-6 mb-4">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">Price: &#8369;{{ product.price }}</p>
            <button @click="addToCart(product)" class="btn btn-primary">Add to Cart</button>
          </div>
        </div>
      </div>
      <nav aria-label="Page navigation">
        <ul class="pagination justify-content-center">
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <button class="page-link" @click="prevPage" :disabled="currentPage === 1">Previous</button>
          </li>
          <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: page === currentPage }">
            <button class="page-link" @click="changePage(page)">{{ page }}</button>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === totalPages }">
            <button class="page-link" @click="nextPage" :disabled="currentPage === totalPages">Next</button>
          </li>
        </ul>
      </nav>
    </div>
  </template>
  
  <script>
  export default {
    props: ['products'],
    data() {
      return {
        currentPage: 1,
        itemsPerPage: 6,
      };
    },
    computed: {
      paginatedProducts() {
        const startIndex = (this.currentPage - 1) * this.itemsPerPage;
        const endIndex = startIndex + this.itemsPerPage;
        return this.products.slice(startIndex, endIndex);
      },
      totalPages() {
        return Math.ceil(this.products.length / this.itemsPerPage);
      },
    },
    methods: {
      addToCart(product) {
        this.$emit('add-to-cart', product);
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
      changePage(page) {
        this.currentPage = page;
      },
    },
  };
  </script>
  