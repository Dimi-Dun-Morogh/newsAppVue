<template>
  <div class="container-lg  ml-auto mr-auto  mt-3">
    <div class="row justify-content-center articlesWrap">
      <div
        class="col-sm-5 mb-3"
        v-for="(article, index) in newsObj"
        :key="index"
      >
        <ArticleCard :article="article" />
      </div>
    </div>
  </div>
</template>

<script>
import ArticleCard from "./ArticleCard";
export default {
  name: "Articles",
  components: { ArticleCard },
  props: ["newsObj"]
};
</script>
<style scoped>
/* @media (max-width:1000px) {
  .articlesWrap{
    flex-direction:column;
  }
} */
</style>
