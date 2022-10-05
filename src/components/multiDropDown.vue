<template>
  <div
    :data="selectedOptions"
    class="container"
    tabindex="0"
    @click="isOpen = !isOpen"
    @blur="isOpen = false"
  >
    <span class="value" v-if="selectedOptions.length"
      ><button
        class="option-badge"
        v-for="option in selectedOptions"
        :key="option.value"
        @click="removeOption(option.value)"
        @click.stop
      >
        {{ option.label }} <span class="clear-btn">&times;</span>
      </button></span
    >
    <span v-else class="value">Click to select options</span>
    <div class="clear-btn" @click.stop @click="clearAllOptions">&times;</div>
    <div class="divider"></div>
    <div class="caret"></div>
    <ul class="options" :class="isOpen ? 'show' : ''">
      <li
        class="option"
        :class="isOptionSelected(option) ? 'selected' : ''"
        @click="addOption(option)"
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
let selectedOptions = ref([]);


// Add options
const addOption = (option) => {
  if (selectedOptions.value.includes(option)) {
    //If option is already selected, unselect it

    removeOption(option.value);
  } else {
    // add option
    selectedOptions.value.push(option);
  }
};

// Clear all selected options
const clearAllOptions = () => {
  selectedOptions.value = [];
};

const removeOption = (optionValue) => {
  // Find the index of the option
  const index = selectedOptions.value.findIndex((object) => {
    return object.value === optionValue;
  });

  // Remove from array
  selectedOptions.value.splice(index, 1);
};

// Highlight the current selected option
const isOptionSelected = (option) => {
  return selectedOptions.value.includes(option);
};
</script>

<style scoped>
.container {
  position: relative;
  width: 20em;
  min-height: 1.5em;
  border: 0.05em solid;
  display: flex;
  align-items: center;
  gap: 0.5em;
  padding: 0.5em;
  border-radius: 0.25em;
  outline: none;
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

.option-badge {
  background-color: rgb(158, 158, 158);
  border: 0.05rem solid;
  display: flex;
  align-items: center;
  border-radius: 0.25rem;
  padding: 0.15rem 0.3rem;
  gap: 0.25rem;
}

.option-badge:hover {
  background-color: hsl(200, 100%, 50%);
  cursor: pointer;
}
</style>
