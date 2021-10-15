<template>
  <div class="weather-side">
    <div class="gradient"></div>
    <div class="date-container">
      <h2 class="day-name">日期</h2>
      <span class="date-day">
        {{ cityInfo.weatherDatas[0].applicable_date }}
      </span>
      <span id="location">
        {{ cityInfo.city }}
      </span>
    </div>

    <div class="weather-container">
      <!-- icon -->
      <span><img :src="imgUrl" alt="" /></span>
      <div class="weather-temp">
        {{ Math.round(cityInfo.weatherDatas[0].the_temp) }}°C
      </div>
      <div class="weather-desc">
        {{ cityInfo.weatherDatas[0].weather_state_name }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WeatherSide",
  props: ["cityInfo"],
  computed: {
    imgUrl() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[0].weather_state_abbr}.svg`;
    },
  },
};
</script>

<style lang="scss" scoped>
$colorBackground: #424242;
$colorContainer: #222831;
$colorGradient: linear-gradient(135deg, #72edf1 10%, #5151e6 100%);
//--- left part start ---
.weather-side {
  position: relative;
  width: 300px;
  height: 100%;
  border-radius: 25px 0 0 25px;
  box-shadow: 0 0 35px -10px rgba(0, 0, 0, 0.2);
}

.gradient {
  position: absolute;
  width: 100%;
  height: 100%;
  background-image: $colorGradient;
  border-radius: 25px 0 0 25px;
  opacity: 0.8;
}

.date-container {
  position: absolute;
  top: 25px;
  left: 25px;

  .date-day {
    display: block;
    margin-top: 4px;
  }

  #location {
    display: block;
    margin-top: 4px;
  }
}

.weather-container {
  position: absolute;
  bottom: 25px;
  left: 25px;

  #Layer_1 {
    transform: scale(0.7);
  }
  .weather-temp {
    font-size: 4em;
    font-weight: bold;
  }
  .weather-desc {
    font-size: 20px;
  }
}
//--- left part end ---
</style>
