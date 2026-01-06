<template>
  <v-container class="d-flex flex-column ga-2">
    <h1 class="text-primary">Events</h1>

    <v-sheet>
      <div class="d-flex justify-space-between pa-2">
        <v-btn
          class="ma-2"
          icon="mdi-chevron-left"
          variant="text"
          @click="prev()"
        />
        <p class="text-h3">{{ title }}</p>
        <v-btn
          class="ma-2"
          icon="mdi-chevron-right"
          variant="text"
          @click="next()"
        />
      </div>

      <v-calendar
        ref="calendar"
        v-model="focus"
        class="mb-4"
        color="primary"
        :events="events"
      />
    </v-sheet>

    <p
      v-if="!focusedMonthEvents.length"
      class="text-center text-body-1 mt-2"
    >
      No events scheduled for {{ title }}
    </p>

    <v-card v-for="event in focusedMonthEvents" :key="event.key">
      <v-card-title class="text-primary">{{ event.name }}</v-card-title>
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

<script setup lang="ts">
  import { ref, computed } from 'vue'

  const calendar = ref<any>(null)
  const focus = ref('') // '' = today
  const title = computed(() => calendar.value?.title ?? '')

  function prev() {
    calendar.value?.prev?.()
  }

  function next() {
    calendar.value?.next?.()
  }

  type EventItem = {
    key: number
    name: string
    start: string
    end: string
    date: string
    time: string
    location: string
  }

  const events = ref<EventItem[]>([
    {
      key: 1,
      name: 'Door Knocking',
      start: '2025-12-07T16:00:00',
      end: '2025-12-07T17:00:00',
      date: 'Sunday, December 7, 2025',
      time: '4:00 PM',
      location: 'Meet in 888 building lobby',
    },
    {
      key: 2,
      name: 'Tenant Union Meeting',
      start: '2025-12-14T12:00:00',
      end: '2025-12-14T13:00:00',
      date: 'Sunday, December 14, 2025',
      time: '12:00 PM',
      location: 'Lucky Labrador\n915 SE Hawthorne Ave',
    },
  ])

  function monthKey(d: Date) {
    return `${d.getFullYear()}-${d.getMonth()}`
  }

  const focusedMonthEvents = computed(() => {
    const focusDate = focus.value
      ? new Date(`${focus.value}T00:00:00`) // force local
      : new Date()

    const key = monthKey(focusDate)

    return events.value
      .map(e => ({ ...e, _start: new Date(e.start) }))
      .filter(e => monthKey(e._start) === key)
      .sort((a, b) => a._start.getTime() - b._start.getTime())
  })
</script>
