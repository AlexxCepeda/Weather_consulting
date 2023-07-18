<script setup>
import { reactive, ref, computed } from "vue";
import axios from "axios";
import iconoSoleado from "./assets/sun.svg";
import iconoNublado from "./assets/cloud.svg";
import Formulario from "./components/Formulario.vue";
import Spinner from "./components/Spinner.vue";
import WeatherCard from "./components/WeatherCard.vue";

const locationTarget = reactive({
  city: "",
  country: "",
});

const weather = ref({});

const key = import.meta.env.VITE_API_KEY;

const options = computed(() => {
  return {
    method: "GET",
    url: "https://weather-by-api-ninjas.p.rapidapi.com/v1/weather",
    params: {
      city: locationTarget.city,
      country: locationTarget.country,
    },
    headers: {
      "X-RapidAPI-Key": key,
      "X-RapidAPI-Host": "weather-by-api-ninjas.p.rapidapi.com",
    },
  };
});

const isFetching = ref(false);

const onFormHandler = async () => {
  isFetching.value = true;
  weather.value = {};
  try {
    const response = await axios.request(options.value);
    weather.value = response.data;
    isFetching.value = false;
  } catch (error) {
    console.error(error);
  }
};

const showResult = computed(() => {
  return Object.values(weather.value).length > 0;
});
</script>

<template>
  <div class="contenedor">
    <header>
      <img :src="iconoSoleado" alt="icono sol" class="iconSunny" />
      <h1 class="title">How is the weather now?</h1>
      <img :src="iconoNublado" alt="icono nubes" class="iconCloudly" />
    </header>
    <div :class="{ result: showResult || isFetching }" class="result-container">
      <Formulario
        @fetch-location="onFormHandler"
        v-model:city="locationTarget.city"
        v-model:country="locationTarget.country"
        class="item-1"
      />
      <Spinner v-if="isFetching" />
      <WeatherCard
        v-if="showResult"
        :target="locationTarget"
        :weather="weather"
      />
    </div>
  </div>
</template>

<style scoped>
header {
  margin-top: 8rem;
  position: relative;
  padding: 2rem;
}
.iconSunny {
  position: absolute;
  width: 170px;
  right: -5px;
  top: -9rem;
  rotate: 32deg;
  z-index: -1;
}
.iconCloudly {
  position: absolute;
  width: 150px;
  z-index: -1;
  top: 4px;
  left: 1rem;
}
.title {
  margin: 0;
  font-weight: 800;
  text-align: center;
  font-size: 62px;
  line-height: 75px;
  letter-spacing: -0.04em;
  background: linear-gradient(
    143deg,
    rgba(255, 248, 0, 1) 0%,
    rgba(22, 193, 242, 1) 60%,
    rgba(41, 35, 231, 1) 100%
  );

  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
.result-container {
  margin-top: 8rem;
  display: flex;
  align-items: center;
  gap: 5rem;
  padding-bottom: 5rem;
}
.result .item-1 {
  flex: 0.5;
}

.item-1 {
  flex: 1;
}

@media screen and (max-width: 550px) {
  header {
    margin-top: 2rem;
  }
  .title {
    font-size: 48px;
    line-height: 60px;
  }
  .iconSunny {
    width: 13rem;
    right: -2rem;
    top: -3rem;
    rotate: -4deg;
  }
  .iconCloudly {
    width: 10rem;
    top: 7.5rem;
    left: 1.2rem;
  }
  .result {
    flex-direction: column;
  }
  .result .item-1 {
    width: 100%;
  }
}
</style>
