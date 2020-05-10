<template>
  <div class="col-sm-3 ml-auto mr-auto  ">
    <div class="">
      <b-form @submit="onSubmit" @reset="onReset" class="">
        <b-form-group
          id="input-group-3"
          label="Chose your Country:"
          label-for="input-3"
        >
          <b-form-select
            id="input-3"
            v-model="form.country"
            :options="countries"
            required
          ></b-form-select>
        </b-form-group>
        <b-form-group id="input-group-2" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.search"
            required
            placeholder="Search"
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
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
        country: "United States"
      },
      countries: [{ text: "United States", value: "United States" }, "Ukraine"]
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.food = null;
      this.form.checked = [];
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>
