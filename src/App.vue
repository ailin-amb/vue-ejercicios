<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div id="app">
    <h1>Ejercicios Vue 3</h1>
    <PasswordValidator />
    <hr />
    <UserFilter />
  </div>
</template>

<script>
import PasswordValidator from './components/PasswordValidator.vue';
import UserFilter from './components/UserFilter.vue';

export default {
  name: 'App',
  components: {
    PasswordValidator,
    UserFilter
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 2em;
}
hr {
  margin: 2em 0;
}
</style>

//Por qué:

//import PasswordValidator trae nuestro componente al nivel de la aplicación.

// <PasswordValidator /> lo renderiza dentro de la página.