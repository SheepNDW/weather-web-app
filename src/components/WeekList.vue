<template>
  <div class="week-container">
    <ul class="week-list">
      <li class="active">
        <!-- icon -->
        <span><img :src="imgUrl" alt="" /></span>
        <span class="day-name">
          {{ cityInfo.weatherDatas[0].applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp">
          {{ Math.round(cityInfo.weatherDatas[0].the_temp) }}°C
        </span>
      </li>
      <li>
        <!-- icon -->
        <span><img :src="imgUrl2" alt="" /></span>
        <span class="day-name">
          {{ cityInfo.weatherDatas[1].applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp">
          {{ Math.round(cityInfo.weatherDatas[1].the_temp) }}°C
        </span>
      </li>
      <li>
        <!-- icon -->
        <span><img :src="imgUrl3" alt="" /></span>
        <span class="day-name">
          {{ cityInfo.weatherDatas[2].applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp">
          {{ Math.round(cityInfo.weatherDatas[2].the_temp) }}°C
        </span>
      </li>
      <li>
        <!-- icon -->
        <span><img :src="imgUrl4" alt="" /></span>
        <span class="day-name">
          {{ cityInfo.weatherDatas[3].applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp">
          {{ Math.round(cityInfo.weatherDatas[3].the_temp) }}°C
        </span>
      </li>
      <li>
        <!-- icon -->
        <span><img :src="imgUrl5" alt="" /></span>
        <span class="day-name">
          {{ cityInfo.weatherDatas[4].applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp">
          {{ Math.round(cityInfo.weatherDatas[4].the_temp) }}°C
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "WeekList",
  props: ["cityInfo"],
  computed: {
    imgUrl() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[0].weather_state_abbr}.svg`;
    },
    imgUrl2() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[1].weather_state_abbr}.svg`;
    },
    imgUrl3() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[2].weather_state_abbr}.svg`;
    },
    imgUrl4() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[3].weather_state_abbr}.svg`;
    },
    imgUrl5() {
      return `https://www.metaweather.com/static/img/weather/${this.cityInfo.weatherDatas[4].weather_state_abbr}.svg`;
    },
  },
};
</script>

<style lang="scss" scoped>
.week-list {
  margin: 10px 35px;
  border-radius: 10px;
  box-shadow: 0 0 50px -5px rgba(0, 0, 0, 0.4);

  display: flex;
  li {
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex: 1;
    padding: 15px;
    cursor: pointer;
    border-radius: 10px;
    text-align: center;
    transition: 0.2s;
    &:hover {
      transform: scale(1.1);
      background-color: #fff;
      color: #222831;
    }

    span {
      display: block;
    }
  }

  .day-name {
    margin-top: 10px;
    text-align: center;
  }
  .day-temp {
    margin-top: 10px;
    text-align: center;
    font-size: 14px;
    font-weight: bold;
  }
}
</style>
