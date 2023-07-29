<template>
    <div class="container">
        <div id="tracker-management-container">
            <button type="button" id="run-tracker" @click="runTracker">Run Tracker</button>
            <button type="button" id="stop-tracker" @click="stopTracker">Stop Tracker</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    methods: {
        async runTracker() {
            try {
                await axios.post('/api/run_tracker');
                console.log("Tracker started.");
            } catch (error) {
                console.error(error);
            }
            },
            async stopTracker() {
            try {
                await axios.post('/api/stop_tracker');
                console.log("Tracker stopped.");
            } catch (error) {
                console.error(error);
            }
        }
    }
}
</script>

<style scoped>
#tracker-management-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    margin: auto 0;
}
#tracker-management-container > button {
    width: 50%;
}
#run-tracker {
    justify-self: end;
}
</style>