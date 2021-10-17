# 天氣預報 App

![image](https://raw.githubusercontent.com/SheepNDW/weather-web-app/master/src/assets/weatherAppDemo.gif)

## 概要

1. 使用 weather data source open API: <a href="https://www.metaweather.com/api/">MetaWeather</a> 結合 Vue.js 框架開發一個天氣預報 Web App
2. 功能：
   1. 預設為台北的天氣
   2. 顯示出最近 5 天的天氣概況：天氣、氣溫、濕度...等
   3. 配合使用者輸入的城市名動態更新天氣資料 (城市僅限 MetaWeather 支援之城市)

## 使用技術&方法

1. 建立 Vue Cli 開發環境 (Vue2)
2. 使用 SCSS 進行樣式開發
3. 使用 axios 來呼叫第三方 api
4. 使用到的 Vue 技術：
   1. 配置代理 server 來解決跨域問題 (devServer.proxy)
   2. 利用 props ､ event bus 以及自定義事件$emit 進行組件間的數據傳遞
   3. 透過綁定樣式 :style 來實現動態更新 bar charts
   4. 透過計算屬性計算濕度百分比 再綁定在樣式動態更新 pie chart
   5. 使用 v-show 操控顯示 Loading 頁面
