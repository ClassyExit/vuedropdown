<template>
  <h3>Single drop down</h3>
  <singleDropDown :options="options"></singleDropDown>

  <h3>Multi drop down</h3>
  <multiDropDown v-bind:value="test" :options="options"></multiDropDown>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

import multiDropDown from "./components/multiDropDown.vue";
import singleDropDown from "./components/singleDropDown.vue";

export default defineComponent({
  name: "App",
  components: { singleDropDown, multiDropDown },
  setup() {
    const options = [
      { label: "First Option", value: 1 },
      { label: "Second Option", value: 2 },
      { label: "Third Option", value: 3 },
      { label: "Fourth Option", value: 4 },
      { label: "Fifth Option", value: 5 },
    ];

    let test: any = [];

    return { options, test };
  },
});
</script>

<style></style>
