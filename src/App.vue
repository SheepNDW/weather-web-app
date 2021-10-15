<template>
  <div class="container">
    <!-- weather(left) -->
    <WeatherSide :cityInfo="cityInfo" />

    <!-- info(right) -->
    <div class="info-side">
      <div class="today-info-container">
        <div class="today-info">
          <!-- MaxT -->
          <div class="MaxT clear">
            <span class="title">最高溫</span>
            <span class="value"
              >{{ Math.round(cityInfo.weatherDatas[0].max_temp) }}°C</span
            >
          </div>
          <!-- MinT -->
          <div class="MinT clear">
            <span class="title">最低溫</span>
            <span class="value"
              >{{ Math.round(cityInfo.weatherDatas[0].min_temp) }}°C</span
            >
          </div>
          <!-- humidity -->
          <div class="humidity clear">
            <span class="title">濕度</span>
            <span class="value">{{ cityInfo.weatherDatas[0].humidity }}%</span>
          </div>
        </div>
      </div>

      <WeekList :cityInfo="cityInfo" />

      <Search />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "./components/Search.vue";
import WeatherSide from "./components/WeatherSide.vue";
import WeekList from "./components/WeekList.vue";

export default {
  name: "App",
  components: {
    Search,
    WeatherSide,
    WeekList,
  },
  data() {
    return {
      cityInfo: {
        city: "Taipei",
        weatherDatas: [
          // {
          //   applicable_date: "2021-10-15",
          //   the_temp: 30.630000000000003,
          //   weather_state_abbr: "lc",
          //   weather_state_name: "Light Cloud",
          //   max_temp: 30.73,
          //   min_temp: 24.835,
          //   humidity: 66,
          // },
          // {
          //   applicable_date: "2021-10-15",
          //   the_temp: 30.630000000000003,
          //   weather_state_abbr: "lc",
          //   weather_state_name: "Light Cloud",
          //   max_temp: 30.73,
          //   min_temp: 24.835,
          //   humidity: 66,
          // },
          // {
          //   applicable_date: "2021-10-15",
          //   the_temp: 30.630000000000003,
          //   weather_state_abbr: "lc",
          //   weather_state_name: "Light Cloud",
          //   max_temp: 30.73,
          //   min_temp: 24.835,
          //   humidity: 66,
          // },
          // {
          //   applicable_date: "2021-10-15",
          //   the_temp: 30.630000000000003,
          //   weather_state_abbr: "lc",
          //   weather_state_name: "Light Cloud",
          //   max_temp: 30.73,
          //   min_temp: 24.835,
          //   humidity: 66,
          // },
          // {
          //   applicable_date: "2021-10-15",
          //   the_temp: 30.630000000000003,
          //   weather_state_abbr: "lc",
          //   weather_state_name: "Light Cloud",
          //   max_temp: 30.73,
          //   min_temp: 24.835,
          //   humidity: 66,
          // },
        ],
      },
    };
  },
  created() {
    axios.get(`http://localhost:8080/api/location/2306179/`).then(
      (response) => {
        // console.log("請求成功了");
        this.cityInfo.weatherDatas = response.data.consolidated_weather;
      },
      (error) => {
        console.log(error.message);
      }
    );
  },
  mounted() {
    this.$bus.$on("updateCityData", (dataObj) => {
      console.log("我是App 我收到citydata");
      this.cityInfo = { ...this.cityInfo, ...dataObj };
    });
  },
};
</script>

<style lang="scss">
$colorBackground: #424242;
$colorContainer: #222831;
$colorGradient: linear-gradient(135deg, #72edf1 10%, #5151e6 100%);

* {
  margin: 0;
  padding: 0;
  list-style: none;
  font-family: Arial, Helvetica, sans-serif;
}

.clear::after {
  content: "";
  display: block;
  clear: both;
}

body {
  width: 100%;
  height: 100vh;
  background-color: $colorBackground;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  position: relative;
  display: flex;
  width: 750px;
  height: 435px;
  background-color: $colorContainer;
  border-radius: 25px;
  box-shadow: 0 0 70px -10px rgba(0, 0, 0, 0.2);
  color: #fff;
}

//--- right part start ---
.info-side {
  width: 450px;
  padding-top: 25px;
  margin-right: 10px;
  height: 100%;
  box-sizing: border-box;
  position: relative;
}

.today-info {
  padding: 15px 15px 0 15px;
  margin: 0 25px 25px 25px;
  box-shadow: 0 0 50px -5px rgba(0, 0, 0, 0.4);
  border-radius: 10px;

  div {
    margin-bottom: 10px;
  }
  .title {
    float: left;
  }
  .value {
    float: right;
  }
}

.active {
  background-color: #fff;
  color: #222831;
}

//--- right part end ---
</style>
