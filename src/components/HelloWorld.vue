<template>
  <v-container class="fill-height" max-width="1200">
    <div>
      <v-img
        class="mb-6"
        cover
        gradient="to top, rgba(0,0,0,.5), rgba(0,0,0,.5)"
        height="260"
        position="50% 40%"
        src="@/assets/doors.jpg"
      >
        <div class="d-flex justify-end align-end text-h2 font-weight-bold h-100 mr-2 mb-2">
          Goat Blocks Tenant Union
        </div>
      </v-img>
      <v-row>
        <v-col v-for="link in links" :key="link.route" cols="12">
          <v-card
            class="py-4"
            color="surface-variant"
            :prepend-icon="link.icon"
            rounded="lg"
            :subtitle="link.subtitle"
            :title="link.title"
            :to="link.route"
            variant="tonal"
          />
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script setup lang="ts">
  const links = [
    {
      route: '/Events',
      icon: 'mdi-calendar',
      subtitle: 'Upcoming meetings and other events',
      title: 'Events',
    },
    {
      route: '/Contact',
      icon: 'mdi-email',
      subtitle: 'Contact us or join our mailing list for updates',
      title: 'Contact',
    },
    {
      route: '/Resources',
      icon: 'mdi-information',
      subtitle: 'Additional tenant resources and information',
      title: 'Resources',
    },
  ]
</script>
