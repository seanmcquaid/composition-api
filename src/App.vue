<template>
  <div>
    <h1>Enter Github User Name</h1>
    <input v-model="name" />
    <button @click="newName = name">Press Me</button>
  </div>
  <ul></ul>
  {{ newName }}
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'App',
  components: {},
  setup() {
    const name = ref(null);
    const newName = ref(null);

    return { name, newName };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
