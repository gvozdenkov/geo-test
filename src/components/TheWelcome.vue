<script setup>
import { google, outlook, office365, yahoo, ics } from 'calendar-link';
import { ref } from 'vue';

const event = {
  title: 'My birthday party',
  description: 'Be there!',
  start: '2025-03-06 18:00:00',
  end: '2025-03-06 19:00:00',
};

const goo = google(event);
const mail = ics(event);
const yandex = `https://calendar.yandex.ru/event?title=${event.title}&start=${event.start}&end=${event.end}&description=${event.description}`;
</script>

<template>
  <a :href="goo">add to Google Calendar</a>
  <br />
  <a :href="yandex">add to Yandex Calendar</a>
  <br />
  <a :href="mail">add to Mail Calendar</a>
  <p>{{ link }}</p>
</template>
