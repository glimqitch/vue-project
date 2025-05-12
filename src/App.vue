<template>
  <div id="app">
    <Header />
    <main>
      <component :is="currentPage" />
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import HomePage from './components/HomePage.vue'
import ApiPage from './components/ApiPage.vue'
import LostMediaPage from './components/LostMediaPage.vue'

export default {
  name: 'App',
  components: {
    Header,
    Footer,
    HomePage,
    ApiPage,
    LostMediaPage
  },
  data() {
    return {
      currentPage: 'HomePage'
    };
  },
  watch: {
    $route(to) {
      this.setPage(to.path);
    }
  },
  methods: {
    setPage(path) {
      if (path === '/') {
        this.currentPage = 'HomePage';
      } else if (path === '/api') {
        this.currentPage = 'ApiPage';
      } else if (path === '/lostmedia') {
        this.currentPage = 'LostMediaPage';
      }
    }
  },
  mounted() {
    this.setPage(window.location.pathname);
  }
};
</script>

<style scoped>
/* Estils generals */
</style>
