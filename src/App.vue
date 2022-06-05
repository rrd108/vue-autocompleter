<script setup>
  import { computed, ref } from 'vue'
  import axios from 'axios'

  const city = ref('')
  const cities = ref([])

  const getCities = () => {
    if (city.value.length > 2) {
      axios
        .get(`https://hur.webmania.cc/zips/${city.value}.json`)
        .then(res => (cities.value = res.data.zips))
        .catch(error => console.error(error))
    }
  }

  const cityNames = computed(() => {
    return [...new Set(cities.value.map(city => city.name))]
  })
</script>

<template>
  Település név
  <input type="search" v-model="city" list="cities" @input="getCities" />
  <datalist id="cities">
    <option v-for="cityName in cityNames">{{ cityName }}</option>
  </datalist>
</template>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    background-color: #ffc499;
    background-image: radial-gradient(
        at 94% 58%,
        hsla(308, 73%, 62%, 1) 0px,
        transparent 50%
      ),
      radial-gradient(at 15% 26%, hsla(270, 66%, 66%, 1) 0px, transparent 50%),
      radial-gradient(at 54% 23%, hsla(255, 96%, 74%, 1) 0px, transparent 50%),
      radial-gradient(at 56% 0%, hsla(56, 92%, 72%, 1) 0px, transparent 50%),
      radial-gradient(at 2% 23%, hsla(307, 97%, 67%, 1) 0px, transparent 50%),
      radial-gradient(at 60% 38%, hsla(347, 63%, 71%, 1) 0px, transparent 50%),
      radial-gradient(at 24% 78%, hsla(0, 71%, 60%, 1) 0px, transparent 50%);
    color: #2c3e50;
    min-height: 100vh;
  }
  body,
  input {
    font-size: 2rem;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin: 4em;
    padding: 1em;
    background-color: #fff;
  }
  #app,
  input {
    border: 0.01em solid #ccc;
    border-radius: 0.5em;
  }
  input {
    padding: 0.25em;
  }
  option {
    width: 100%;
  }
</style>
