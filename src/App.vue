<template>
  <section id="app-vue" :class="typeof res.main != 'undefined' && res.main.temp > 16 ? 'warm' : '' ">
    <main>
      <img alt="Vue logo" src="./assets/logo.png" />
      <HomeVue />
      <input
        type="text"
        v-on:change="searchLocation"
        v-model="search_input"
        name="search"
        id="search"
        class="search-box"
      />
      <div class="box" v-if="typeof res.main != 'undefined'">
        <div class="location">{{ res.name }}</div>
        <div class="temp">{{ Math.round(res.main.temp) }}</div>
        <div class="situation">{{ res.weather[0].main }}</div>
      </div>
    </main>
  </section>
</template>

<script>
import HomeVue from "./components/Home.vue"
import axios from 'axios'
export default {
  name: 'App',
  components: {
    HomeVue
  },
  data() {
    return {
      search_input: "",
      api_key: "3fea3e7c70c7526b6ddcb8c42e189831",
      url: "http://api.openweathermap.org/data/2.5/weather",
      res: {}
    }
  },
  methods: {
    searchLocation() {
      //const data = axios.get(this.url + "?q=" + this.search_input + "&APPID=" + this.api_key)
      axios.get(`${this.url}?q=${this.search_input}&APPID=${this.api_key}&units=metric`)
        .then(results => {
          this.res = results.data;
          console.log(results.data);
        })


    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: #fff;
}
#app-vue {
  background-image: url("./assets/images/cold.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  text-align: center;
  margin: auto;
}
#app-vue.warm {
  background-image: url("./assets/images/warm.jpg");
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}
h1 {
  color: white;
}
.search-box {
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  margin-top: 30px;
  margin-bottom: 5px;
}

.temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.situation {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
