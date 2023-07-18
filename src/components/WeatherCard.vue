<script setup>
import hotIcon from "../assets/hotIcon.svg";
import coldIcon from "../assets/coldIcon.svg";

const iconsDict = {
  hotDay: hotIcon,
  coldDay: coldIcon,
};
const props = defineProps({
  city: {
    type: String,
    required: true,
  },
  weather: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="card animated slideInRight">
    <h3 class="title">Weather in {{ city }}</h3>
    <div class="card-flex">
      <div class="card_image-content">
        <img :src="iconsDict.coldDay" alt="icono clima" />
      </div>
      <div class="card_text-content">
        <p>
          Temp: <span>{{ weather.temp }} °C</span>
        </p>
        <p>
          Max temp: <span>{{ weather.max_temp }} °C</span>
        </p>
        <p>
          Min temp: <span>{{ weather.min_temp }} °C</span>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  padding: 3rem;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  padding: 3rem;
  border-radius: 1rem;
  height: 244.06px;
  width: 100%;
}
.card-flex {
  margin-top: 4rem;
  display: flex;
  align-items: center;
  justify-content: space-around;
}
img {
  width: 90px;
}
.title {
  font-size: 2.2rem;
  margin: 0;
  text-align: center;
}
.card_text-content p {
  font-size: 1.2rem;
  letter-spacing: 0.04em;
  font-weight: 800;
}
.card_text-content span {
  font-weight: 400;
}
@-webkit-keyframes slideInRight {
  from {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

@keyframes slideInRight {
  from {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    visibility: visible;
  }

  to {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
}

.slideInRight {
  -webkit-animation-name: slideInRight;
  animation-name: slideInRight;
}

.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
@media screen and (max-width: 550px) {
  .card {
    height: auto;
  }
}
</style>
