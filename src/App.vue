<template>
  <Title />
  <Form @submit-form="getWeather" />
  <Results />
  {{ results }}
</template>

<script setup>
import { reactive } from "vue";
import axios from 'axios';
import Title from './components/Title.vue';
import Form from './components/Form.vue';
import Results from './components/Results.vue';

const results = reactive({
  country: "",
  cityName: "",
  temperature: "",
  conditionText: "",
  icon: ""
});

const getWeather = () => {
  axios
    .get(
      'http://api.weatherapi.com/v1/current.json?key=acab368a978240028be51642232108&q=London&aqi=no',
    )
  .then((res) => {
    results.country = res.data.location.country,
    results.cityName = res.data.location.name,
    results.temperature = res.data.current.temp_c,
    results.conditionText = res.data.current.condition.text,
    results.icon = res.data.current.condition.icon
  });
};
</script>
