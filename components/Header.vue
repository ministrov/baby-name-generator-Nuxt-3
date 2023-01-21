<template>
  <header class="header">
    <a class="header__logo" href="#">
      LOgo
    </a>

    <SelectLang/>
  </header>
</template>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 50rem;
  margin: 0 auto;
  padding: 1rem 2rem;
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  box-sizing: border-box;
}

.header__logo {
  display: flex;
  text-decoration: none;
}
</style>