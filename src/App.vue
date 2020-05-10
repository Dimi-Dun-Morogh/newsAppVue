<template>
  <div id="app">
    <Header />
    <Toaster :lastUrl="lastUrl" />
    <Form @FormSent="getNews" />
    <div class="text-center" v-show="spinnerVisible">
      <b-spinner label="Spinning"></b-spinner>
    </div>
    <Articles :newsObj="newsObj" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Form from "./components/Form";
import Articles from "./components/Articles";
import Toaster from "./components/Toast";
export default {
  name: "App",
  components: { Header, Form, Articles, Toaster },
  data() {
    return {
      newsObj: {},
      spinnerVisible: false,
      lastUrl: ""
    };
  },
  mounted: function() {
    this.getNews({
      search: "",
      country: "Ukraine",
      category: "technology"
    });
  },
  methods: {
    getNews(obj = {}) {
      let { search, country, category } = obj;
      let countries = {
        "United States": "us",
        Ukraine: "ua",
        Russia: "ru"
      };
      const xhr = new XMLHttpRequest();
      const apiKey = "6085543a03c1460b933f2b17e2a32b2b";
      const apiUrl = "https://newsapi.org/v2";
      this.spinnerVisible = true;
      // let category = "technology";
      if (!search) {
        this.lastUrl = `${apiUrl}/top-headlines?country=${countries[country] ||
          "us"}&category=${category}&apiKey=${apiKey}`;
        xhr.open("GET", this.lastUrl);
      } else {
        this.lastUrl = `${apiUrl}/everything?q=${search}&apiKey=${apiKey}`;
        xhr.open("GET", this.lastUrl);
      }

      xhr.addEventListener("load", () => {
        const response = JSON.parse(xhr.response);
        console.log(response);
        this.newsObj = response.articles;
        this.spinnerVisible = false;
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
  background-color: #f9f9fa;
}
</style>
