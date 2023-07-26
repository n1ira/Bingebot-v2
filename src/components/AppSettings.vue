<template>
  <div class="container">
    <h1>App Settings</h1>
    <form @submit.prevent="saveSettings">
      <label>
        Download Directory:
        <input type="text" v-model="settings.download_dir" />
      </label>
      <label>
        Torrent Type:
        <select v-model="settings.torrent_type" multiple>
          <option value="success">Success</option>
          <option value="danger">Danger</option>
          <option value="default">Default</option>
        </select>
      </label>
      <label>
        Poll Interval (seconds):
        <input type="number" v-model="settings.poll_interval_seconds" />
      </label>
      <label>
        Seek Missing Episodes:
        <input type="checkbox" v-model="settings.will_seek_missing_episodes" />
      </label>
      <label>
        Seek Missing Episodes Interval (seconds):
        <input type="number" v-model="settings.seek_missing_episodes_interval_seconds" />
      </label>
      <label>
        Seek Newest Episode:
        <input type="checkbox" v-model="settings.will_seek_newest_episode" />
      </label>
      <label>
        Seek Newest Episode Interval (seconds):
        <input type="number" v-model="settings.seek_newest_episode_interval_seconds" />
      </label>
      <label>
        Torrent Quality:
        <input type="text" v-model="settings.torrent_quality" />
      </label>
      <label>
        Torrent Providers Whitelist:
        <input type="text" v-model="settings.torrent_providers_whitelist" />
      </label>
      <label>
        Torrent Client URL:
        <input type="text" v-model="settings.torrent_client_url" />
      </label>
      <label>
        Torrent Client Username:
        <input type="text" v-model="settings.torrent_client_username" />
      </label>
      <label>
        Torrent Client Password:
        <input type="password" v-model="settings.torrent_client_password" />
      </label>
      <button type="submit">Save</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'AppSettings',
  data() {
    return {
      settings: {},
    };
  },
  async created() {
    const response = await axios.get('/api/settings');
    this.settings = response.data;
  },
  methods: {
    async saveSettings() {
      await axios.put('/api/settings/1', this.settings);
    },
  },
};
</script>
