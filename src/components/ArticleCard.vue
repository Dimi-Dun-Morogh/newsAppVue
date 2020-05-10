<template>
  <div class="articleWrap ">
    <div
      class="
  img-card-wrap"
      :style="imgBg"
    >
      <div class="title-overlay">
        <b-card-title class="pl-1">{{ article.title }}</b-card-title>
      </div>

      <!-- "
  { background:`url(${article.urlToImage})`} -->
    </div>
    <div class="d-flex flex-column mt-2 ">
      <div class="description">
        <p class="text-left pl-2">
          {{ article.description || "no description avalaible" }}
        </p>
      </div>

      <div class="align-self-end mr-auto ml-1 mt-1">
        <b-button :href="article.url" variant="info" class=""
          >Read More</b-button
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ArticleCard",
  props: ["article"],
  computed: {
    imgBg: function() {
      return {
        background:
          this.article.urlToImage != null
            ? `url(${this.article.urlToImage})`
            : `linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(178,57,217,1) 72%, rgba(0,212,255,0.9724090319721639) 100%)`,
        backgroundSize: `cover`
      };
    }
  },
  mounted: function() {
    console.log(this.imgBg);
  }
};
</script>
<style scoped>
/* .card-img-top{
  width: 300px;
  height: 300px;
} */
.img-card-wrap {
  width: 450px;
  height: 200px;
  background-image: url();
  background-size: cover;
  border-radius: 5px 5px 0 0;
}
.articleWrap {
  box-shadow: 1px 1px 1px 1px #00000026;
  width: 450px;
  height: 330px;
  border-radius: 5px;
  /* border: 1px solid #1a050575; */
}
.description {
  display: block;
  height: 70px;
  overflow: hidden;
}
.title-overlay {
  color: #fff;
  background-color: rgba(0, 0, 0, 0.459);
  border-radius: 5px 5px 0 0;
}
</style>
