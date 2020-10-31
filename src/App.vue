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
import { computed, onMounted, reactive, ref, toRefs, watch } from 'vue';
import Axios from 'axios';

export default {
  name: 'App',
  components: {},
  setup() {
    // EASY way to think of ref vs reactive - ref = primitive, reactive = object
    const name = ref(null);
    const newName = ref(null);
    const state = reactive({ data: [] });
    const computedValue = computed(() => name.value + ' STEVE');

    onMounted(() => {
      console.log('make an api call here on load!');
    });

    watch(() => {
      // sort of like an observable, only runs this when any dependencies change
      Axios.get(`https://api.github.com/users/${newName.value}/repos`).then(
        ({ data }) => {
          state.data = data;
          name.value;
        }
      );
    });

    const changeName = () => {
      newName.value = name.value;
    };

    return {
      name,
      newName,
      computedValue,
      changeName,
      ...toRefs(state),
    };
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
