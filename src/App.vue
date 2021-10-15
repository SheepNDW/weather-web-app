<template>
  <div class="container">
    <!-- weather(left) -->
    <WeatherSide />

    <!-- info(right) -->
    <div class="info-side">
      <div class="today-info-container">
        <div class="today-info">
          <!-- percent -->
          <div class="percent clear">
            <span class="title">降雨率</span>
            <span class="value">88</span>
          </div>
          <!-- humidity -->
          <div class="humidity clear">
            <span class="title">濕度</span>
            <span class="value">88</span>
          </div>
          <!-- wind -->
          <div class="wind clear">
            <span class="title">風速</span>
            <span class="value">88</span>
          </div>
        </div>
      </div>

      <WeekList />

      <Search />
    </div>
  </div>
</template>

<script>
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
        city: {},
        weatherDatas: {},
      },
    };
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
  width: 700px;
  height: 435px;
  background-color: $colorContainer;
  border-radius: 25px;
  box-shadow: 0 0 70px -10px rgba(0, 0, 0, 0.2);
  color: #fff;
}

//--- right part start ---
.info-side {
  width: 400px;
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
