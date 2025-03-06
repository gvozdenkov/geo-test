<script setup>
import { google, outlook, office365, yahoo, ics } from 'calendar-link';
import { ref } from 'vue';

const event = {
  title: 'My birthday party',
  description: 'Be there!',
  start: '2025-03-06 18:00:00 +0100',
  duration: [3, 'hour'],
};

const link = google(event);

if ('geolocation' in navigator) {
  const options = {
    enableHighAccuracy: true,
    timeout: 5000,
    maximumAge: 0,
  };
  // Геолокация доступна
  navigator.geolocation.getCurrentPosition(successCallback, errorCallback, options);
} else {
  console.log('Геолокация не поддерживается вашим браузером');
}

const locationStr = ref('');

function successCallback(position) {
  const latitude = position.coords.latitude;
  const longitude = position.coords.longitude;
  locationStr.value = `${latitude}, ${longitude}`;
  console.log(`Широта: ${latitude}, Долгота: ${longitude}`);
}

function errorCallback(error) {
  switch (error.code) {
    case error.PERMISSION_DENIED:
      console.log('Пользователь отказал в доступе к геолокации');
      break;
    case error.POSITION_UNAVAILABLE:
      console.log('Информация о местоположении недоступна');
      break;
    case error.TIMEOUT:
      console.log('Запрос на получение местоположения превысил время ожидания');
      break;
    case error.UNKNOWN_ERROR:
      console.log('Произошла неизвестная ошибка');
      break;
  }
}
</script>

<template>
  <a :href="link">add to Google Calendar</a>
  <p>{{ link }}</p>
  <p>location:</p>
  <p>{{ locationStr }}</p>
</template>
