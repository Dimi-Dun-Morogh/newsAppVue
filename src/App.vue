<template>
  <div id="app">
    <Header />
    <Form @FormSent="getNews" />
    <Articles :newsObj="newsObj" />
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
    this.getNews({
      search: "",
      country: "Ukraine"
    });
  },
  methods: {
    getNews(obj = {}) {
      let { search, country } = obj;
      let countries = {
        "United States": "us",
        Ukraine: "ua"
      };
      const xhr = new XMLHttpRequest();
      const apiKey = "6085543a03c1460b933f2b17e2a32b2b";
      const apiUrl = "https://newsapi.org/v2";
      // let category = "technology";
      if (!search) {
        xhr.open(
          "GET",
          `${apiUrl}/top-headlines?country=${countries[country] ||
            "us"}&category=technology&apiKey=${apiKey}`
        );
      } else {
        xhr.open("GET", `${apiUrl}/everything?q=${search}&apiKey=${apiKey}`);
      }

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
