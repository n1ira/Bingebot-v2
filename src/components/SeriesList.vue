<template>
  <div class="container">
    <div id="new-anime">
      <input v-model="newSeriesName" type="text" placeholder="New series name">
      <button type="button" @click="addSeries">Add Series</button>
    </div>
    <ul>
      <li v-for="series in seriesList" :key="series.id">
        <div class="series-name" contenteditable="true" @blur="editSeriesName($event, series.id)" @keydown.enter.prevent="editSeriesName($event, series.id)">
          {{ series.name }}
        </div>
        <div class="episode-number">
          <input class="episode-input" v-model.number="series.last_episode_downloaded" type="number" min="0" placeholder="Last episode downloaded" @input="updateEpisodeNumber(series.id, series.last_episode_downloaded)">
        </div>
        <div class="remove-button">
          <button type="button" @click="removeSeries(series.id)">Remove</button>
        </div>
      </li>
    </ul>
  </div>
</template>


<script>
import axios from 'axios';
import _ from 'lodash';

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
    updateEpisodeNumber: _.debounce(async function(id, last_episode_downloaded) {
      try {
        await axios.put(`/api/series/${id}`, { last_episode_downloaded });
        const updatedSeries = this.seriesList.find(series => series.id === id);
        if (updatedSeries) {
          updatedSeries.last_episode_downloaded = last_episode_downloaded;
        }
      } catch (error) {
        console.error(error);
      }
    }, 500),
    editSeriesName(event, seriesId) {
      const newName = event.target.innerText;
      this.updateSeriesName(seriesId, newName);
    },

    async updateSeriesName(id, newName) {
      try {
        await axios.put(`/api/series/${id}`, { name: newName });
        const updatedSeries = this.seriesList.find(series => series.id === id);
        if (updatedSeries) {
          updatedSeries.name = newName;
        }
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

<style scoped>
li {
  list-style-type: none;
  display: flex;
  align-items: stretch; /* changed from 'center' to 'stretch' */
  justify-content: space-between;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
}
#new-anime {
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 10px;
}
.series-name {
  /* make series-name float left and fixed width */
  float: left;
  width: 70%; 
  word-wrap: break-word;
  padding: 4px;
  display: flex;
  align-items: center;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #ececec;
}

li > button {
  width: 90px;
}
.episode-input {
  width: 37px !important;
}
</style>