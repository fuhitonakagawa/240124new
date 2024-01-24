<!-- <template>
  <div>
    <h1>天気予報</h1>
    <select v-model="selectedRegion">
    <option v-for="(code, region) in regions" :key="code" :value="code">
      {{ region }}
    </option>
  </select>
    <button @click="fetchWeather">天気を取得</button>

    <div v-if="weather">
      <h2>{{ weather.targetArea }}</h2>
      <p>{{ weather.text }}</p>
    </div>
  </div>
</template> -->

<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">天気予報</h1>
    <div class="row justify-content-center mb-4">
      <div class="col-md-4">
        <select v-model="selectedRegion" class="form-select">
          <option v-for="(code, region) in regions" :key="code" :value="code">
            {{ region }}
          </option>
        </select>
      </div>
      <div class="col-md-2">
        <button @click="fetchWeather" class="btn btn-primary w-100">天気を取得</button>
      </div>
    </div>

    <div v-if="weather" class="weather-display mt-4">
      <table class="table table-bordered">
        <tr>
          <th>発表機関</th>
          <td>{{ weather.publishingOffice }}</td>
        </tr>
        <tr>
          <th>発表日時</th>
          <td>{{ weather.reportDatetime }}</td>
        </tr>
        <tr>
          <th>対象地域</th>
          <td>{{ weather.targetArea }}</td>
        </tr>
        <tr>
          <th>天気概要</th>
          <td>{{ weather.headlineText }}</td>
        </tr>
        <tr>
          <th>詳細</th>
          <td>{{ weather.text }}</td>
        </tr>
      </table>
    </div>

    <p v-else class="text-center text-muted">天気情報はありません</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'WeatherForecast',
  data() {
    return {
      selectedRegion: '130000',
      regions: {
        '茨城県': '080000',
        '栃木県': '090000',
        '群馬県': '100000',
        '埼玉県': '110000',
        '東京都': '130000',
        '千葉県': '120000',
        '神奈川県': '140000',
        '長野県': '200000',
        '山梨県': '190000'
      },
      weather: null
    };
  },
  methods: {
    fetchWeather() {
      const url = `https://www.jma.go.jp/bosai/forecast/data/overview_forecast/${this.selectedRegion}.json`;
      axios.get(url)
        .then(response => {
          this.weather = response.data;
        })
        .catch(error => {
          console.error('Error:', error);
        });
    }
  }
}
</script>
