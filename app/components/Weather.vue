<template>
  <Page class="page">
    <ActionBar title="Погода" class="action-bar">
      <NavigationButton
        text="Назад"
        android.systemIcon="ic_menu_back"
        @tap="goBack"
      />
    </ActionBar>
    <ScrollView>
      <FlexboxLayout flexDirection="column">
        <SearchBar
          hint="Введите город"
          v-model="city"
          @submit="getCoordinate"
        />
        <Label text="Информация о погоде" />
        <Label
          v-if="weatherInfo.main.temp"
          :text="`Температура: ${weatherInfo.main.temp}`"
        />
        <Label
          v-if="weatherInfo.main.feels_like"
          :text="`Ощущается как: ${weatherInfo.main.feels_like}`"
        />
        <Label
          v-if="weatherInfo.main.temp_min"
          :text="`Минимальная: ${weatherInfo.main.temp_min}`"
        />
        <Label
          v-if="weatherInfo.main.temp_max"
          :text="`Максимальная: ${weatherInfo.main.temp_max}`"
        />
      </FlexboxLayout>
    </ScrollView>
  </Page>
</template>

<script>
import { Http } from "@nativescript/core";

import Home from "./Home.vue";

export default {
  name: "Weather",
  methods: {
    getCoordinate() {
      Http.getJSON(
        `https://api.openweathermap.org/geo/1.0/direct?q=${this.city}&appid=${this.apiKey}`
      ).then((res) => {
        this.cityInfo = res[0];
        this.getWeather();
      });
    },
    getWeather() {
      Http.getJSON(
        `https://api.openweathermap.org/data/2.5/weather?lat=${this.cityInfo.lat}&lon=${this.cityInfo.lon}&lang=ru&appid=${this.apiKey}&units=metric`
      ).then((res) => {
        this.weatherInfo = res;
      });
    },
    goBack() {
      this.$navigateTo(Home);
    },
  },

  data() {
    return {
      city: "",
      apiKey: "f7daafb088af09b6c1d12d3ed4f29a7e",
      cityInfo: {},
      weatherInfo: {
        coord: {
          lon: null,
          lat: null,
        },
        weather: [
          {
            id: null,
            main: null,
            description: null,
            icon: null,
          },
        ],
        base: "stations",
        main: {
          temp: null,
          feels_like: null,
          temp_min: null,
          temp_max: null,
          pressure: null,
          humidity: null,
        },
        visibility: null,
        wind: {
          speed: null,
          deg: null,
        },
        clouds: {
          all: null,
        },
        dt: null,
        sys: {
          type: null,
          id: null,
          country: null,
          sunrise: null,
          sunset: null,
        },
        timezone: null,
        id: null,
        name: null,
        cod: null,
      },
      url: "",
    };
  },
};
</script>

<style scoped></style>
