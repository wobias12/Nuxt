<template>
  <div>
    <button @click="fetchData">Daten abrufen</button>
    <h1>Nuxt Spike</h1>
    <div v-if="dataLoaded">
      <h2>Daten aus der Datenbank:</h2>
      <ul>
        <li v-for="event in events" :key="event.id">{{ event }}</li>
      </ul>
      
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  data() {
    return {
      events: [],
      dataLoaded: false
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch('http://localhost:8080/event'); 
        const data = await response.json();
        this.events = data;
        this.dataLoaded = true;
      } catch (error) {
        console.error('Fehler beim Abrufen der Daten:', error);
      }
    }
  }
});
</script>
