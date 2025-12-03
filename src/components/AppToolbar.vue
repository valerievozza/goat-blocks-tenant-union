<template>
  <v-app-bar :elevation="2">

    <template #append>
      <div class="d-flex ga-2">
        <v-btn active-color="primary" text="Home" to="/" />
        <v-btn active-color="primary" text="Events" to="/Events" />
        <v-btn active-color="primary" text="Contact" to="/Contact" />
        <v-btn active-color="primary" text="Resources" to="/Resources" />
      </div>
    </template>
  </v-app-bar>
</template>
