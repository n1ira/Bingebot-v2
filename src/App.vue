<template>
    <div class="app-container">
        <h1 id="title">BingeBot</h1>
        <SeriesList/>
        <TrackerManagement/>
        <AppSettings/>
    </div>
</template>

<script>
import SeriesList from './components/SeriesList.vue'
import TrackerManagement from './components/TrackerManagement.vue'
import AppSettings from './components/AppSettings.vue'

export default {
    name: 'App',
    components: {
        SeriesList,
        TrackerManagement,
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

#title {
    text-align: center;
}

label {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
}
label > div {
    display: flex;
    align-items: center;
    gap: 10px;
}

form {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
}

input[type="text"], input[type="number"], input[type="password"], select {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 10px;
    font-size: 1em;
}

button {
    padding: 10px 16px;
    background-color: #007BFF;
    color: #fff;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 1em;
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