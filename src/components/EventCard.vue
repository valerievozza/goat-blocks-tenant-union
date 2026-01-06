<template>
  <v-card>
    <v-card-title class="text-primary">{{ event.name }}</v-card-title>
    <v-card-subtitle>
      <p><span class="font-weight-medium">Date:</span> {{ event.date }}</p>
      <p><span class="font-weight-medium">Time:</span> {{ event.time }}</p>
    </v-card-subtitle>
    <v-card-text>
      <p><span class="font-weight-medium">Location:</span> {{ event.location }}</p>
    </v-card-text>
  </v-card>
</template>

<script setup lang="ts">
  import type { EventItem } from '@/types/EventItem'

  const props = defineProps<{
    event: EventItem
  }>()
</script>
