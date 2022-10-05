<template>
  <div
    class="container"
    tabindex="0"
    @click="isOpen = !isOpen"
    @blur="isOpen = false"
  >
    <span class="value">{{ isSelected.label }}</span>
    <div class="clear-btn" @click.stop @click="clearSelected">&times;</div>
    <div class="divider"></div>
    <div class="caret"></div>
    <ul class="options" :class="isOpen ? 'show' : ''">
      <li
        class="option"
        :class="isOptionSelected(option) ? 'selected' : ''"
        @click="selectOption(option)"
        v-for="option in props.options"
        :key="option.value"
      >
        {{ option.label }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  options: {
    type: Array,
    default: () => [],
  },
});

const isOpen = ref(false);
let isSelected = ref({ label: "Click to select an option", value: false });

// Selected option
const selectOption = (option) => {
  isSelected.value = option;
};

// Clear Selected Option
const clearSelected = () => {
  isSelected.value = {};
};

// Highlight the current selected option
const isOptionSelected = (option) => {
  return option.value === isSelected.value.value;
};
</script>

<style scoped>
.container {
  position: relative;
  width: 20rem;
  min-height: 1.5rem;
  display: flex;
  align-items: center;
  border: 2px solid;
  gap: 0.5rem;
  padding: 0.5rem;
  border-radius: 0.25rem;
}

.container:focus {
  border-color: hsl(200, 100%, 50%);
}

.value {
  flex-grow: 1;
  display: flex;
  gap: 0.5em;
  flex-wrap: wrap;
}

.divider {
  background-color: #777;
  align-self: stretch;
  width: 0.05em;
}

.caret {
  translate: 0 25%;
  border: 0.25em solid transparent;
  border-top-color: #777;
  cursor: pointer;
}

.clear-btn {
  background: none;
  color: rgb(177, 2, 2);
  cursor: pointer;
  font-size: 1.25rem;
  font-weight: bold;
}

.clear-btn:focus,
.clear-btn:hover {
  color: red;
}

.options {
  position: absolute;
  margin: 0;
  padding: 0;
  max-height: 15rem;
  overflow-y: auto;
  border: 0.05rem solid;
  width: 100%;
  left: 0;
  top: calc(100% + 0.25rem);
  z-index: 100;
  background-color: white;
  display: none;
}

.options.show {
  display: block;
}

.option {
  padding: 0.25em 0.5em;
  cursor: pointer;
}

.option.selected {
  background-color: hsl(200, 100%, 60%);
}
.option:hover {
  background-color: hsl(200, 100%, 90%);
}
</style>
