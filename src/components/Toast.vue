<template>
  <div class="toaster">
    <b-button class="mb-2" @click="toast('b-toaster-top-right')">
      <b-icon icon="question-square"></b-icon>
    </b-button>

    <b-toast id="example-toast" title="BootstrapVue" static no-auto-hide>
      Hello, world! This is a toast message.
    </b-toast>
  </div>
</template>
<script>
export default {
  name: "Toaster",
  props: ["lastUrl"],
  methods: {
    toast(toaster, append = false) {
      this.$bvToast.toast(`${this.lastUrl.slice(0, -32)}h3h3h3h3h3`, {
        title: `Последний отправленный запрос:`,
        toaster: toaster,
        solid: true,
        appendToast: append
      });
    }
  }
};
</script>
<style scoped>
.toaster {
  float: right;
}
</style>
