<template>
  <v-container>
    <v-layout text-center wrap>

      <v-toolbar color="teal">
        <v-toolbar-title>Search Name</v-toolbar-title>
        <v-autocomplete
          v-model="select"
          :loading="loading"
          :items="items"
          :search-input.sync="search"
          cache-items
          class="mx-4"
          flat
          hide-no-data
          hide-details
          label="Type here"
          solo-inverted
        ></v-autocomplete>
      </v-toolbar>

    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: "AutoComplete",
  data() {
    return {
      loading: false,
      items: [],
      search: null,
      select: null,
      states: [],
    };
  },
  watch: {
    search(val) {
      this.items=[];
      val && val !== this.select && this.querySelections(val);
    }
  },
  methods: {
    querySelections(v) {
      if (v.length <= 2) return;
      this.loading = true;
      fetch("http://localhost:4200/names?q=" + v)
        .then(res => res.json())
        .then(res => {
          this.items = res.map(
            value =>
              value.givenName + " " + value.middleName + " " + value.surname
          );
          this.loading = false;
        });
    }
  }
};
</script>
