<template>
  <div id="app">
    <div class="container" v-show="!cityInfo.isLoading">
      <!-- weather(left) -->
      <WeatherSide :cityInfo="cityInfo" :currentSelect="currentSelect" />

      <!-- info(right) -->
      <div class="info-side">
        <div class="today-info-container">
          <div class="today-info">
            <!-- MaxT -->
            <div class="MaxT clear">
              <span class="title">最高溫</span>
              <span class="value"
                >{{ Math.round(currentSelect.max_temp) }}°C</span
              >
            </div>
            <!-- MinT -->
            <div class="MinT clear">
              <span class="title">最低溫</span>
              <span class="value"
                >{{ Math.round(currentSelect.min_temp) }}°C</span
              >
            </div>
            <!-- humidity -->
            <div class="humidity clear">
              <span class="title">濕度</span>
              <span class="value">{{ currentSelect.humidity }}%</span>
            </div>
          </div>
        </div>

        <WeekList :cityInfo="cityInfo" @getCurrentActive="updateShow" />

        <Search />
      </div>
    </div>
    <!-- 載入中&錯誤提示 -->
    <div class="loadingPage" v-show="cityInfo.isLoading">
      <div class="monster">
        <div class="eye">
          <div class="eyeBall"></div>
        </div>
        <div class="mouth"></div>
      </div>
      <h2 v-show="!cityInfo.errMsg">Loading...</h2>
      <h2 v-show="cityInfo.errMsg">{{ cityInfo.errMsg }}</h2>
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
        isLoading: false,
        errMsg: "",
        city: "Taipei",
        weatherDatas: [],
      },
      currentSelect: [],
    };
  },
  created() {
    axios.get(`http://localhost:8080/api/location/2306179/`).then(
      (response) => {
        this.cityInfo.weatherDatas = response.data.consolidated_weather;
        this.currentSelect = response.data.consolidated_weather[0];
      },
      (error) => {
        console.log(error.message);
      }
    );
  },
  mounted() {
    this.$bus.$on("updateCityData", (dataObj) => {
      this.cityInfo = { ...this.cityInfo, ...dataObj };
    });
  },
  methods: {
    updateShow(dataObj) {
      this.currentSelect = dataObj;
    },
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

.loadingPage {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 750px;
  height: 435px;
  background-color: $colorContainer;
  border-radius: 25px;
  color: #fff;

  .monster {
    width: 110px;
    height: 110px;
    background-color: #e55a54;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column;
    cursor: pointer;
    margin: 10px;
    position: relative;
    box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
    transition: 0.5s;
    animation: jumping 0.8s infinite alternate;

    .eye {
      width: 40%;
      height: 40%;
      border-radius: 50%;
      background-color: white;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .eyeBall {
      width: 50%;
      height: 50%;
      border-radius: 50%;
      background-color: #0c4475;
    }

    .mouth {
      width: 32%;
      height: 12px;
      background-color: white;
      border-radius: 12px;
      margin-top: 15%;
    }

    &:before,
    &:after {
      content: "";
      display: block;
      width: 20%;
      height: 10px;
      background-color: white;
      position: absolute;
      left: 50%;
      top: -10px;
      border-radius: 10px;
    }

    &:before {
      transform: translateX(-70%) rotate(45deg);
    }

    &:after {
      transform: translateX(-30%) rotate(-45deg);
    }

    &.blue {
      background-color: #0c4475;
      animation-delay: 0.5s;

      .mouth,
      .eyeBall {
        background-color: #e55a54;
      }
    }
  }
  @keyframes jumping {
    50% {
      top: 0;
      box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
    }
    100% {
      top: -50px;
      box-shadow: 0px 120px 50px rgba(0, 0, 0, 0.2);
    }
  }
  @keyframes eyeMove {
    0%,
    10% {
      transform: translate(50%);
    }
    90%,
    100% {
      transform: translate(-50%);
    }
  }
  .monster .eyeBall {
    animation: eyeMove 1.6s infinite alternate;
  }
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

//--- right part end ---
</style>
