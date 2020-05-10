<template>
  <div id="app">
    <Header />
    <Form />
    <Articles />
  </div>
</template>

<script>
import Header from "./components/Header";
import Form from "./components/Form";
import Articles from "./components/Articles";
export default {
  name: "App",
  components: { Header, Form, Articles },
  data() {
    return {
      newsObj: {}
    };
  },
  mounted: function() {
    this.getNews();
  },
  methods: {
    getNews() {
      const xhr = new XMLHttpRequest();
      const apiKey = "6085543a03c1460b933f2b17e2a32b2b";
      const apiUrl = "https://newsapi.org/v2";
      // let category = "technology";
      xhr.open("GET", `${apiUrl}/top-headlines?country=us&apiKey=${apiKey}`);
      xhr.addEventListener("load", () => {
        const response = JSON.parse(xhr.response);
        console.log(response);
        this.newsObj = response.articles;
      });
      xhr.send();
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
