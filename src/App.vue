<template>
  <div id="app">
    <MuseumPage type="space" />
  </div>
</template>

<script>
import MuseumPage from "./components/MuseumPage.vue";

export default {
  name: "App",
  components: {
    MuseumPage,
  },
};
</script>

<style>
:root {
  --clr-card-primary: #f3f4f6;
  --clr-card-highlight: #ffe4e6;
  --clr-news-border: #d1d5db;
  --clr-news-bg: #e8eaef;
  --border-radius: 0.25rem;
}
#app {
  display: flex;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
img {
  max-width: 100%;
}
h1,
h2,
h3,
h4,
h5,
h6,
p {
  margin: 0;
}
p {
  margin: 0;
}
</style>
