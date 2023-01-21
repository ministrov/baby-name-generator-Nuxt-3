<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find  Names" button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />

      <button class="primary"
        @click="computeSelectedNames"
      >Find Names
      </button>
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

<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";

interface OptionsState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
};

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  length: Length.SHORT,
  popularity: Popularity.TRENDY,
});

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    })

    selectedNames.value = filteredNames.map((name) => name.name);
};

const selectedNames = ref<string[]>([]);

const removeName = (index: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1);
  selectedNames.value = filteredNames
}

const optionsArray = [
  {
    title: '1) Choose a gender',
    category: 'gender',
    buttons: [Gender.BOY, Gender.UNISEX, Gender.GIRL]
  },
  {
    title: '2) Choose a name\'s popularity',
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE]
  },
  {
    title: '3) Choose a name\'s length',
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG]
  }
];

</script>

<style scoped>
.container {
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
  color: rgb(27, 60, 138);
  font-family: Arial, Helvetica, sans-serif;
}

h1 {
  font-size: 3rem;
}

.options-container {
  position: relative;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  padding: 1rem;
  padding-bottom: 3rem;
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
}

.options-container {
  margin-bottom: 2rem;
}

.option {
  width: 12rem;
  padding: 0.75rem;
  font-size: 1rem;
  font-weight: 200;
  color: rgb(27, 60, 138);
  background: white;
  border: none;
  outline: 0.15rem solid rgb(249, 87, 89);
  cursor: pointer;
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

.primary {
  margin-top: 2.2rem;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  color: white;
  background-color: rgb(249, 87, 89);
  border: none;
  border-radius: 6.5rem;
  cursor: pointer;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}
/* 200 lines of code */
</style>
