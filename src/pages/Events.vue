<template>
  <v-container class="d-flex flex-column ga-2">
    <h1 class="text-primary">Upcoming Events</h1>
    <v-card v-for="event in events" :key="event.key">
      <v-card-title class="text-primary">{{ event.title }}</v-card-title>
      <v-card-subtitle>
        <p><span class="font-weight-medium">Date:</span> {{ event.date }}</p>
        <p><span class="font-weight-medium">Time:</span> {{ event.time }}</p>
      </v-card-subtitle>
      <v-card-text>
        <p><span class="font-weight-medium">Location:</span> {{ event.location }}</p>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script lang="ts" setup>
  import { ref } from 'vue'

  const events = ref([
    {
      key: 1,
      title: 'Door Knocking',
      date: 'Sunday, December 7, 2025',
      time: '4:00 PM',
      location: 'Meet in 888 building lobby',
    },
    {
      key: 2,
      title: 'Tenant Union Meeting',
      date: 'Sunday, December 14, 2025',
      time: '12:00 PM',
      location: 'Lucky Labrador\n915 SE Hawthorne Ave',
    },
  ])
</script>
