<template>
  <div class="week-container">
    <ul class="week-list">
      <li
        v-for="(day, index) in cityInfo.weatherDatas.slice(0, 5)"
        :key="index"
      >
        <span
          ><img
            :src="`https://www.metaweather.com/static/img/weather/${day.weather_state_abbr}.svg`"
            alt=""
        /></span>
        <span class="day-name">
          {{ day.applicable_date.slice(5, 10) }}
        </span>
        <span class="day-temp"> {{ Math.round(day.the_temp) }}°C </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "WeekList",
  props: ["cityInfo"],
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
