<template>
  <div>
    <input v-model="newSeriesName" type="text" placeholder="New series name">
    <button @click="addSeries">Add Series</button>
    <ul>
      <li v-for="series in seriesList" :key="series.id">
        {{ series.name }}
        <button @click="removeSeries(series.id)">Remove</button>
        <!-- Add update input field and button -->
        <input v-model.number="series.last_episode_downloaded" type="number" min="0" placeholder="Last episode downloaded">
        <button @click="updateSeries(series.id, series.last_episode_downloaded)">Update</button>
      </li>
    </ul>
  </div>
  <div>
    <button @click="runTracker">Run Tracker</button>
  </div>
</template>


<script>
import axios from 'axios';

export default {
  data() {
    return {
      newSeriesName: '',
      seriesList: []
    };
  },
  methods: {
    async addSeries() {
      try {
        const response = await axios.post('/api/series', { series_name: this.newSeriesName, last_episode_downloaded : 0});
        this.seriesList.push(response.data.series);
        this.newSeriesName = '';
      } catch (error) {
        console.error(error);
      }
    },
    async removeSeries(id) {
      try {
        await axios.delete(`/api/series/${id}`);
        this.seriesList = this.seriesList.filter(series => series.id !== id);
      } catch (error) {
        console.error(error);
      }
    },
    async getSeries() {
      try {
        const response = await axios.get('/api/series');
        this.seriesList = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async updateSeries(id, last_episode_downloaded) {
      try {
        await axios.put(`/api/series/${id}`, { last_episode_downloaded });
        const updatedSeries = this.seriesList.find(series => series.id === id);
        if (updatedSeries) {
          updatedSeries.last_episode_downloaded = last_episode_downloaded;
        }
      } catch (error) {
        console.error(error);
      }
    },
    async runTracker() {
      try {
        const response = await axios.post('/api/series/run_tracker');
        console.log("Tracker run successfully.");
        console.log("Updated seriesList:", response.data);
      } catch (error) {
        console.error(error);
      }
    }
  },
  created() {
    this.getSeries();
  }
}
</script>
