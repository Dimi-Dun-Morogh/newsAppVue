<template>
  <div
    class="col-sm-5 col-md-5 col-lg-4 ml-auto mr-auto d-flex flex-column form_wrap"
  >
    <div class=" col-sm-11 mt-3 ml-auto mr-auto">
      <h1 class="display-4">Search News</h1>
      <b-form @submit="onSubmit" @reset="onReset" class="">
        <b-form-group
          class="text-left text-secondary "
          id="input-group-3"
          label="Chose your Country:"
          label-for="input-3"
          label-class="mb-0 small"
        >
          <b-form-select
            id="input-3"
            v-model="form.country"
            :options="countries"
            required
          ></b-form-select>
        </b-form-group>
        <b-form-group
          class="text-left text-secondary "
          id="input-group-4"
          label="Chose your Category:"
          label-for="input-4"
          label-class="mb-0 small"
        >
          <b-form-select
            id="input-4"
            v-model="form.category"
            :options="categories"
          ></b-form-select>
        </b-form-group>
        <b-form-group
          class="text-left text-secondary"
          id="input-group-2"
          label-for="input-2"
          label="Search"
          label-class="mb-0 small"
        >
          <b-form-input
            id="input-2"
            v-model="form.search"
            placeholder="Search"
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" class="form_button mr-auto mb-1" variant="info">
          <b-icon icon="search"></b-icon> Search</b-button
        >
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      form: {
        search: "",
        country: "Ukraine",
        category: ""
      },
      countries: [
        { text: "Ukraine", value: "Ukraine" },
        "United States",
        "Russia"
      ],
      categories: [
        { text: "technology", value: "technology" },
        "health",
        "business",
        "general",
        "sports",
        "entertainment"
      ]
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.$emit("FormSent", this.form);
      //alert(JSON.stringify(this.form));
      this.form.search = "";
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.search = "";
      this.form.country = null;
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>
<style scoped>
.form_wrap {
  box-shadow: 1px 1px 1px 1px #00000026;
  background-color: #fff;
}
.form_button {
  display: block;
}
.display-4 {
  font-size: 1.9rem;
  font-weight: 100;
  line-height: 1.2;
}
</style>
