<script setup lang="ts">
import {Gender, Popularity, Length, names} from "~/data";

interface OptionsState {
  gender: String;
  popularity: String;
  length: String;
}

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT,
});

const selectedNames = ref<string[]>([]);

const computedNames = () => {
  const filteredNames = names
      .filter(name => name.gender === options.gender)
      .filter(name => name.popularity === options.popularity)
      .filter(name => {
        if (options.length === Length.ALL) {
          console.log(true)
          return true
        }
        else return name.length === options.length
      });

  selectedNames.value = filteredNames.map(name => name.name);
}

</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options-container">

      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button
              class="option option-left"
              :class="options.gender === Gender.BOY && 'option-active'"
              @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
              class="option"
              :class="options.gender === Gender.UNISEX && 'option-active'"
              @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
              class="option option-right"
              :class="options.gender === Gender.GIRL && 'option-active'"
              @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>2) Choose the name's popularity</h4>
        <div class="option-buttons">
          <button
              class="option option-left"
              :class="options.popularity === Popularity.TRENDY && 'option-active'"
              @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
              class="option option-right"
              :class="options.popularity === Popularity.UNIQUE && 'option-active'"
              @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>3) Choose the name's length</h4>
        <div class="option-buttons">
          <button
              class="option option-left"
              :class="options.length === Length.LONG && 'option-active'"
              @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
              class="option"
              :class="options.length === Length.ALL && 'option-active'"
              @click="options.length = Length.ALL"
          >
            All
          </button
          >
          <button
              class="option option-right"
              :class="options.length === Length.SHORT && 'option-active'"
              @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button class="primary" @click="computedNames">Find Names</button>
    </div>
    {{ selectedNames }}
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 139);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 4rem auto 0;
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
  color: rgb(27, 69, 138);
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

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
</style>
