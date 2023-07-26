<template>
  <SeriesList/>
  <AppSettings/>
</template>

<script>
import SeriesList from './components/SeriesList.vue'
import AppSettings from './components/AppSettings.vue'

export default {
  name: 'App',
  components: {
    SeriesList,
    AppSettings
  }
}
</script>

<style>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f5f5f5;
    color: #333;
}

.container {
    width: 80%;
    margin: 0 auto;
    padding: 20px;
}

h1 {
    color: #444;
    font-size: 2em;
    margin-bottom: 20px;
}

form {
    display: flex;
    flex-direction: column;
}

label {
    display: flex;
    flex-direction: column;
    margin-bottom: 10px;
}

input[type="text"], input[type="number"], input[type="password"], select {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    font-size: 1em;
}

button {
    padding: 10px 20px;
    background-color: #007BFF;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1em;
    margin-top: 20px;
}

button:hover {
    background-color: #0056b3;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #fff;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 4px;
}

li button {
    margin-left: 10px;
}
</style>