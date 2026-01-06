<template>
  <v-footer
    app
    height="40"
  >
    <a
      v-for="item in items"
      :key="item.title"
      class="d-inline-block mx-2 text-decoration-none on-surface"
      :href="item.href"
      rel="noopener noreferrer"
      target="_blank"
      :title="item.title"
    >
      <v-icon
        class="social-link mr-1"
        size="20"
      >{{ item.icon }}</v-icon>
      {{ item.title }}
    </a>
  </v-footer>
</template>

<script setup lang="ts">
  const items = [
    {
      title: 'Contact Us',
      icon: `mdi-email`,
      href: 'mailto:goatblockstenantunion@gmail.com',
    },
  ]
</script>

<style scoped lang="sass">
  .social-link :deep(.v-icon)
    color: rgba(var(--v-theme-on-background), var(--v-disabled-opacity))
    text-decoration: none
    transition: .2s ease-in-out

    &:hover
      color: rgba(25, 118, 210, 1)
</style>
