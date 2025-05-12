<template>
  <div class="api-container">
    <h2 class="page-title">API Data</h2>
    <ul v-if="apiData.length" class="data-list">
      <li v-for="item in apiData" :key="item.id" class="data-item">
        <div class="item-content">
          <h3 class="item-title">{{ item.title }}</h3>
          <p class="item-description">{{ item.body }}</p>
        </div>
      </li>
    </ul>
    <p v-else class="loading-message">Carregant dades...</p>
  </div>
</template>

<script>
export default {
  name: 'ApiPage',
  data() {
    return {
      apiData: []
    };
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/posts')
      .then(response => response.json())
      .then(data => {
        this.apiData = data;
      });
  }
};
</script>

<style scoped>
/* Main container styling */
.api-container {
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #f7f9fc;
  border-radius: 8px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
}

/* Page title styling */
.page-title {
  text-align: center;
  font-size: 2rem;
  color: #333;
  margin-bottom: 20px;
}

/* Loading message */
.loading-message {
  text-align: center;
  font-size: 1.2rem;
  color: #888;
}

/* List styling */
.data-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

/* Individual item styling */
.data-item {
  background-color: #fff;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.data-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
}

/* Inner content container */
.item-content {
  padding: 20px;
}

/* Item title styling */
.item-title {
  font-size: 1.5rem;
  color: #333;
  font-weight: 600;
  margin-bottom: 10px;
}

/* Item description styling */
.item-description {
  font-size: 1rem;
  color: #666;
  line-height: 1.6;
  margin-bottom: 15px;
  word-wrap: break-word;
}

/* Responsive Design */
@media (max-width: 768px) {
  .api-container {
    padding: 15px;
  }

  .page-title {
    font-size: 1.8rem;
  }

  .data-item {
    padding: 15px;
  }
}
</style>
