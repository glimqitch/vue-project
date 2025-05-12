<template>
  <header>
    <nav>
      <ul>
        <li><a href="/" @click.prevent="changePage('/')">Home</a></li>
        <li><a href="/api" @click.prevent="changePage('/api')">API</a></li>
        <li><a href="/lostmedia" @click.prevent="changePage('/lostmedia')">Lost Media</a></li>
      </ul>
    </nav>
  </header>
  <br>
</template>

<script>
export default {
  name: 'Header',
  methods: {
    changePage(page) {
      window.history.pushState(null, '', page);
      this.$root.setPage(page)
    }
  }
};
</script>

<style scoped>
header {
  background-color:rgb(185, 185, 185);
  padding: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

nav ul {
  display: flex;
  list-style-type: none;
  padding: 0;
  margin: 0;
}

nav li {
  margin-right: 20px;
}

a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  padding: 5px;
  border-radius: 4px;
}

a:hover {
  text-decoration: underline;
  color: #007BFF;
}

.active {
  color: #fff;
  background-color: #007BFF;
}
</style>