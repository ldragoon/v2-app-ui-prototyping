<!--
  References: 
    https://codepen.io/pen/?editors=1010
    https://vuetifyjs.com/en/components/autocompletes/#cryptocurrency-selector
-->

<template>
  <section class="p-8">
    <h2 class="pb-4">Autocomplete Component</h2>
    <v-toolbar>
      <v-autocomplete
        v-model="select"
        :items="items"
        :loading="isLoading"
        :search-input.sync="search"
        hide-no-data
        hide-selected
        item-text="Description"
        item-value="Template"
        label="Templates"
        placeholder="search for a template"
        prepend-inner-icon="fa fa-search"
        return-object
      ></v-autocomplete>
    </v-toolbar>
  </section>
</template>

<script>
export default {
  name: "Autocomplete",

  data: () => ({
    isLoading: false,
    items: [],
    search: null,
    select: null,
    templates: [
      "customer_registration",
      "forgot_password",
      "first_delivery_attempt",
      "second_delivery_attempt",
      "third_delivery_attempt",
      "final_delivery_attempt",
      "apartmentDelivery_is_ready",
      "unit_is_occupied",
      "hold_manager",
    ],
  }),
  watch: {
    search(val) {
      val && val !== this.select && this.querySelections(val);
    },
  },
  methods: {
    querySelections(v) {
      this.isLoading = true;

      // Simulated ajax query
      setTimeout(() => {
        this.items = this.templates.filter((e) => {
          return (e || "").toLowerCase().indexOf((v || "").toLowerCase()) > -1;
        });
        this.isLoading = false;
      }, 500);
    },
  },
};
</script>
