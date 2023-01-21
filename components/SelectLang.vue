<template>
  <form class="select-lang">
    <label class="select-lang__label" for="locale-select">Switch the language </label>
    <select id="locale-select">
      <option value="ru">ru</option>
      <option value="en">en</option>
      <option value="fr">fr</option>
    </select>
  </form>
</template>

<style scoped>
.select-lang {
  display: flex;
  flex-direction: column;
}
</style>