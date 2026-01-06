<template>
  <v-container class="d-flex flex-column ga-2">
    <h1 class="text-primary">Events</h1>

    <v-card>
      <div class="d-flex justify-space-between pa-2">
        <v-btn
          class="ma-2"
          icon="mdi-chevron-left"
          variant="text"
          @click="prev()"
        />
        <p class="text-h3">{{ month }}</p>
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
        @click:event="onEventClick"
      />
    </v-card>

    <p
      v-if="focusedMonthEvents.length === 0"
      class="text-center text-body-1 mt-2"
    >
      No events scheduled for {{ month }}
    </p>

    <EventCard
      v-for="event in focusedMonthEvents"
      :key="event.key"
      :event="event"
    />

    <v-dialog v-model="show" max-width="400px">
      <EventCard
        v-if="selectedEvent"
        :event="selectedEvent"
      />
    </v-dialog>
  </v-container>
</template>

<script setup lang="ts">
  import type { EventItem } from '@/types/EventItem'
  import { computed, ref } from 'vue'
  import EventCard from '@/components/EventCard.vue'

  const calendar = ref<any>(null)
  const focus = ref('') // '' = today
  const month = computed(() => calendar.value?.title ?? '')

  const show = ref(false)
  const selectedEvent = ref<EventItem | null>(null)

  function prev () {
    calendar.value?.prev?.()
  }

  function next () {
    calendar.value?.next?.()
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

  function onEventClick (native: Event, cal: any) {
    const clicked = cal?.event ?? cal

    const found = events.value.find(e => String(e.key) === String(clicked?.id ?? clicked?.key))
      ?? events.value.find(e => e.name === (clicked?.name ?? clicked?.title) && e.start === clicked?.start)
      ?? null

    selectedEvent.value = found
    show.value = !!found

    native?.stopPropagation?.()
  }

  function monthKey (d: Date) {
    return `${d.getFullYear()}-${d.getMonth()}`
  }

  const focusedMonthEvents = computed(() => {
    const focusDate = focus.value ? new Date(`${focus.value}T00:00:00`) : new Date()
    const key = monthKey(focusDate)

    return events.value
      .map(e => ({ ...e, _start: new Date(e.start) }))
      .filter(e => monthKey(e._start) === key)
      .sort((a, b) => a._start.getTime() - b._start.getTime())
  })
</script>
