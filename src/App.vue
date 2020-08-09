<template>
  <div id="app">
    <Header />
    <Toaster :lastUrl="lastUrl" />
    <Form @FormSent="getNews" />
    <div class="text-center spinner-wrap" v-show="spinnerVisible">
      <b-spinner
        label="Spinning"
        style="width: 3rem; height: 3rem;"
        type="grow"
      ></b-spinner>
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
    async getNews(obj = {}) {
      let { search, country, category } = obj;
      let countries = {
        "United States": "us",
        Ukraine: "ua",
        Russia: "ru"
      };
      try {
        const apiKey = "6085543a03c1460b933f2b17e2a32b2b";
        const apiUrl = "https://news-api-v2.herokuapp.com";
        this.spinnerVisible = true;

        if (!search) {
          this.lastUrl = `${apiUrl}/top-headlines?country=${countries[
            country
          ] || "us"}&category=${category}&apiKey=${apiKey}`;
        } else {
          this.lastUrl = `${apiUrl}/everything?q=${search}&apiKey=${apiKey}`;
        }
        const response = await fetch(this.lastUrl);
        const data = await response.json();
        this.newsObj = data.articles;
        this.spinnerVisible = false;
      } catch (error) {
        console.log(error);
      }
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
.spinner-wrap {
  margin-top: 40px;
}
</style>
