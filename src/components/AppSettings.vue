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
        <div>
          <input type="checkbox" v-model="settings.torrent_type.success">
          <label>Success</label>
        </div>
        <div>
          <input type="checkbox" v-model="settings.torrent_type.danger">
          <label>Danger</label>
        </div>
        <div>
          <input type="checkbox" v-model="settings.torrent_type.default">
          <label>Default</label>
        </div>
      </label>
      <label>
        Poll Interval (seconds):
        <input type="number" v-model="settings.poll_interval_seconds" />
      </label>
      <label>
          Seek Missing Episodes:
          <input type="checkbox" v-model="settings.will_seek_missing_episodes">
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
        Torrent Providers Whitelist:
        <div v-for="provider in ['nyaa.si', 'otherProvider1', 'otherProvider2']" :key="provider">
          <input type="checkbox" :value="provider" v-model="settings.torrent_providers_whitelist">
          <label>{{ provider }}</label>
        </div>
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
      settings: {
        download_dir: "",
        torrent_type: {
          success: false,
          danger: false,
          default: false,
        },
        torrent_quality: {
          '480': false,
          '720': false,
          '1080': false,
        },
        torrent_providers_whitelist: []
        // ... other settings properties ...
      }
    }
  },
  async created() {
    const response = await axios.get('/api/settings');
    const settings = response.data;

    // Do not join the whitelist into a string
    // settings.torrent_providers_whitelist = settings.torrent_providers_whitelist.join(', ');

    this.settings = settings;
  },
  methods: {
    async saveSettings() {
      // If settings.torrent_providers_whitelist is not an array, convert it to array
      if (typeof this.settings.torrent_providers_whitelist === 'string') {
          this.settings.torrent_providers_whitelist = this.settings.torrent_providers_whitelist.split(', ');
      }
          
      await axios.put(`/api/settings/1`, this.settings);
    },
  },
}
</script>