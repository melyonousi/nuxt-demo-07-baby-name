<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";
// enum Gender {
//   GIRL = "Girl",
//   BOY = "Boy",
//   UNISEX = "Unisex",
// }

// enum Popularity {
//   TRENDY = "Trendy",
//   UNIQUE = "Unique",
// }

// enum Length {
//   SHORT = "Short",
//   LONG = "Long",
//   ALL = "All",
// }
interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

const options = reactive<OptionsState>({
  gender: Gender.BOY,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT,
});

const computeSelectedNames = () => {
  const filterNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) {
        return true;
      } else {
        return name.length === options.length;
      }
    });
  selectedNames.value = filterNames.map((name) => name.name);
};
const selectedNames = ref<string[]>([]);

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames;
};

const optionsArray = [
  {
    title: "1) Choose a Gender",
    category: "gender",
    buttons: [Gender.BOY, Gender.UNISEX, Gender.GIRL],
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length",
    category: "length",
    buttons: [Length.LONG, Length.ALL, Length.SHORT],
  },
];
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Nmaes" button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />
      <button class="primary" v-text="'Find Names'" @click="computeSelectedNames()" />
    </div>
    <div class="cards-container">
      <CardName
        v-for="(name, index) in selectedNames"
        :key="name"
        :name="name"
        @remove="() => removeName(index)"
        :index="index"
      />
    </div>
  </div>
</template>

<style scoped>
* {
  font-family: Arial, Helvetica, sans-serif;

  transition-property: all;
  transition-duration: 1.5s;
  transition-timing-function: cubic-bezier(0.72, 0.73, 0.39, 0.88);
  transition-delay: 0.1s;
}
.container {
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}
.container h1 {
  font-size: 3rem;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
  gap: 1rem;
}
</style>
