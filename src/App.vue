<template>
  <div>
    <h1>Enter Github User Name</h1>
    <input v-model="name" />
    <button @click="newName = name">Press Me</button>
  </div>
  <ul>
    <li v-for="lib in data" :key="lib.name">{{ lib.name }}</li>
  </ul>
</template>

<script>
import { reactive, ref, toRefs, watch } from 'vue';
import Axios from 'axios';

export default {
  name: 'App',
  components: {},
  setup() {
    const name = ref(null);
    const newName = ref(null);
    const state = reactive({ data: [] });

    watch(() => {
      Axios.get(`https://api.github.com/users/${newName.value}/repos`).then(
        ({ data }) => {
          state.data = data;
          name.value;
        }
      );
    });

    return { name, newName, ...toRefs(state) };
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
