<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find  Names" button below</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1 Choose a gender</h4>
        <div class="option-button">
          <button class="option option-left"
          :class="options.gender === Gender.BOY && 'option-active'"
          @click="options.gender = Gender.BOY"
          >Boy
          </button>
          <button class="option"
          :class="options.gender === Gender.UNISEX && 'option-active'"
          @click="options.gender = Gender.UNISEX"
          >Unisex
          </button>
          <button class="option option-right"
          :class="options.gender === Gender.GIRL && 'option-active'"
          @click="options.gender = Gender.GIRL"
          >Girl
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>2 Choose a name's popularity</h4>
        <div class="option-button">
          <button class="option option-left"
          :class="options.popularity === Popularity.TRENDY && 'option-active'"
          @click="options.popularity = Popularity.TRENDY"
          >Trendy
          </button>
          <button class="option option-right"
          :class="options.popularity === Popularity.UNIQUE && 'option-active'"
          @click="options.popularity = Popularity.UNIQUE"
          >Unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>3 Choose a name's length</h4>
        <div class="option-button">
          <button class="option option-left"
          :class="options.length === Length.LONG && 'option-active'"
          @click="options.length = Length.LONG"
          >Long
          </button>
          <button class="option"
          :class="options.length === Length.ALL && 'option-active'"
          @click="options.length = Length.ALL"
          >All
          </button>
          <button class="option option-right"
          :class="options.length === Length.SHORT && 'option-active'"
          @click="options.length = Length.SHORT"
          >Short
          </button>
        </div>
      </div>
      <button class="primary"
      @click="computeSelectedNames"
      >Find Names
      </button>
    </div>
    <div class="cards-container">
      <div v-for="name in selectedNames" key="name" class="card">
        <h4>{{ name }}</h4>
        <p>x</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length, names } from '@/data';

interface OptionsState {
  gender: Gender,
  popularity: Popularity,
  length: Length
}

const obj: OptionsState = {
  gender: Gender.GIRL,
  popularity: Popularity.TRENDY,
  length: Length.ALL
}

const options: OptionsState = reactive({
  gender: Gender.GIRL,
  popularity: Popularity.TRENDY,
  length: Length.ALL
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
}

const selectedNames = ref<string[]>([]);

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

.card {
  position: relative;
  width: 28%;
  margin-right: 0.4rem;
  margin-bottom: 1rem;
  padding: 0.1rem;
  color: white;
  background-color: rgb(27, 60, 138);
  border-radius: 1rem;
}

.card p {
  position: absolute;
  top: -17%;
  left: 91.5%;
  color: rgba(255, 255, 255, 0.178);
  cursor: pointer;
}

/* 200 lines of code */
</style>
