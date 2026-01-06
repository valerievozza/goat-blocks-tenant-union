<template>
  <v-container class="d-flex flex-column ga-4">
    <h1 class="text-primary">Get Involved</h1>

    <form
      data-netlify="true"
      method="POST"
      name="get-involved"
      netlify-honeypot="bot-field"
      @submit.prevent="onSubmit"
    >
      <input name="form-name" type="hidden" value="get-involved">
      <input name="bot-field" type="hidden">

      <v-text-field
        v-model="email"
        color="primary"
        label="Email"
        name="email"
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
        name="firstName"
        required
        :rules="[(v: string) => !!v || 'First name is required']"
        variant="outlined"
      />

      <v-text-field
        v-model="lastName"
        color="primary"
        label="Last Name"
        name="lastName"
        required
        :rules="[(v: string) => !!v || 'Last name is required']"
        variant="outlined"
      />

      <v-textarea
        v-model="message"
        color="primary"
        label="Message (optional)"
        name="message"
        variant="outlined"
      />

      <v-checkbox
        v-model="subscribe"
        color="primary"
        label="Subscribe to our newsletter"
        name="subscribe"
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

  async function onSubmit () {
    const body = new URLSearchParams({
      'form-name': 'get-involved',
      'email': email.value,
      'firstName': firstName.value,
      'lastName': lastName.value,
      'message': message.value,
      'subscribe': subscribe.value ? 'yes' : 'no',
    }).toString()

    await fetch('/', {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body,
    })
  }
</script>
