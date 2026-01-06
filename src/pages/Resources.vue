<template>
  <v-container class="d-flex flex-column">
    <h1 class="text-primary">Resources</h1>
    <v-card
      v-for="resource in resources"
      :key="resource.title"
      class="mt-4"
      :title="resource.title"
    >
      <v-card-text>
        <a :href="resource.link" target="_blank">{{ resource.link }}</a>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script setup lang="ts">
  const resources = [
    {
      title: 'Letter of Demands',
      link: '[Insert link here]',
    },
    {
      title: 'Portland Tenants United',
      link: 'https://www.pdxtu.org/',
    },
  ]
</script>
