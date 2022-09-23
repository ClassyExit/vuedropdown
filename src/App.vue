<template>
  <DropDown :mode="'single'" :options="options" />
  <button @click="">CLick</button>
  <h1>{{}}</h1>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import DropDown from "./components/DropDown.vue";

export default defineComponent({
  name: "App",
  components: { DropDown },
  setup() {
    const options = [
      { label: "First", value: 1 },
      { label: "Second", value: 2 },
      { label: "Third", value: 3 },
      { label: "Fourth", value: 4 },
      { label: "Fifth", value: 5 },
    ];

    return { options };
  },
});
</script>

<style></style>
