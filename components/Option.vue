<script setup lang="ts">
import { Gender, Length, Popularity } from "@/data";

interface OptionProps {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Popularity[] | Length;
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}
const props = defineProps<OptionProps>();

const computeButtonClassess = (value, index) => {
  const classNames = [];
  if (props.options[props.option.category] === value) {
    classNames.push("option-active");
  }

  if (index === 0) {
    classNames.push("option-left");
  }

  if (index === props.option.buttons.length - 1) {
    classNames.push("option-right");
  }

  return classNames.join(" ");
};
</script>

<template>
  <div class="option-container">
    <h4 v-text="option.title" />
    <div class="option-buttons">
      <div class="option-button">
        <button
          v-for="(btnValue, index) in option.buttons"
          :key="btnValue"
          class="option"
          :class="computeButtonClassess(btnValue, index)"
          v-text="btnValue"
          @click="options[option.category] = btnValue"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.option-container {
  margin-bottom: 2rem;
}

.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}
.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}

/* .option-button .option:first-child {
  border-radius: 1rem 0 0 1rem;
}

.option-button .option:last-child {
  border-radius: 0 1rem 1rem 0;
} */
</style>
