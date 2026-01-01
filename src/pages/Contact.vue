<template>
  <v-container class="d-flex flex-column ga-4">
    <h1 class="text-primary">Get Involved</h1>
    <form
      method="POST"
      netlify
      @submit.prevent
    >
      <v-text-field
        v-model="email"
        color="primary"
        label="Email"
        required
        :rules="[
          (v: string) => !!v || 'Email is required',
          (v: string) => /.+@.+\..+/.test(v) || 'Email must be valid',
        ]"
        variant="outlined"
      />

      <v-text-field
        v-model="firstName"
        color="primary"
        label="First Name"
        required
        :rules="[(v: string) => !!v || 'First name is required']"
        variant="outlined"
      />

      <v-text-field
        v-model="lastName"
        color="primary"
        label="Last Name"
        required
        :rules="[(v: string) => !!v || 'Last name is required']"
        variant="outlined"
      />

      <v-textarea
        v-model="message"
        color="primary"
        label="Message (optional)"
        variant="outlined"
      />

      <!-- placeholder="Questions? Comments? Let us know!" -->

      <v-checkbox
        v-model="subscribe"
        color="primary"
        label="Subscribe to our newsletter"
      />

      <v-btn
        color="primary"
        text="Submit"
        type="submit"
      />
    </form>
  </v-container>
</template>

<script lang="ts" setup>
  import { ref } from 'vue'

  const email = ref('')
  const firstName = ref('')
  const lastName = ref('')
  const message = ref('')
  const subscribe = ref(false)
</script>
