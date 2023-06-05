<template>
  <div>
    <div class="absolute left-[400px] top-[-100px] text-orange-500 text-l">
      <p class="">{{ errorMessage }}</p>
    </div>
    <div class="flex justify-center items-center ml-96 mt-[-74px]">
      <input
        class="w-96 h-12 border bg-yellow-50 border-violet-900 rounded-tl-md rounded-bl-md pl-2 focus:outline-none focus:border-sky-500 focus:ring-sky-500"
        placeholder="Search city..."
        v-model="q"
        type="text"
      />
      <button
        v-on:click="error"
        class="w-16 h-12 border border-violet-900 bg-orange-400 rounded-tr-md rounded-br-md pr-2 pl-2 text-white ml-[-1px] focus:outline-none focus:border-sky-500 focus:ring-sky-500"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="pl-2 w-8 h-8"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
          />
        </svg>
      </button>
    </div>

    <div
      class="mt-5 mb-12 ml-96 border shadow-md min-h-[280px] w-[470px] shadow-cyan-500/50 rounded-md"
    >
      <div
        class="rounded-tl-md rounded-tr-md w-[470px] h-[150px] bg-gradient-to-r from-green-400 to-green-400 font-serif border border-violet-900 relative"
      >
        <img
          class="opacity-90 w-full h-full"
          src="./components/icons/city.jpg"
          alt=""
        />

        <div class="absolute top-0 pl-3 text-l w-[450px] h-[150px] text-white">
          <div class="flex justify-end pr-12 pt-6">
            <p class="pt-3 text-xl font-bold">
              <u>{{ form.name }}</u>
            </p>
          </div>
          <div v-if="form.lon" class="flex justify-start">
            <p class="pl-24 text-6xl mt-[-40px]">{{ form.temp }}</p>
            <p class="pl-1 text-5xl mt-[-30px]">°</p>
          </div>
          <div v-if="form.lon" class="flex justify-start text-gray-300">
            <p class="pl-10 mt-2">Latitude</p>
            <div
              class="ml-[120px] mt-3 w-[1px] h-10 absolute bg-gray-400"
            ></div>
            <p class="pl-10 mt-2">Longitude</p>
          </div>
          <div class="flex justify-start text-gray-300 font-mono">
            <p class="pl-6 text-l">{{ form.lat }}</p>
            <p class="text-l pl-6">{{ form.lon }}</p>
          </div>
        </div>
      </div>
      <div class="flex justify-start pt-10 pb-10 pl-5">
        <div class="absolute mt-[-20px]">
          <img class="w-24 h-24" src="./components/icons/Logo.png" alt="" />
        </div>
        <!-- <p class="ml-[-15px] font-mono text-xl font-bold pr-1">Iman</p>
        <h1 class="font-mono text-xl font-bold">Bajalan</h1> -->
        <div
          class="ml-[113px] mt-[-20px] w-[1px] h-24 absolute bg-gray-400"
        ></div>
        <div v-if="form.lon" class="flex">
          <div
            class="flex justify-start text-black font-sanrif ml-28 mt-[-30px] font-bold font-sans"
          >
            <strong>
              <p class="pl-3 font-bold">CO</p>
            </strong>
            <p class="pl-7 font-bold">
              NH<sub class="align-middle font-bold">3</sub>
            </p>
            <p class="pl-9 font-bold">NO</p>
            <p class="pl-8 font-bold">
              NO<sub class="align-middle font-bold">2</sub>
            </p>
            <p class="pl-8 font-bold">
              O<sub class="align-middle font-bold">3</sub>
            </p>
            <p class="pl-7 font-bold">
              SO<sub class="align-middle font-bold">2</sub>
            </p>
          </div>
          <div class="absolute flex">
            <ComponentsIcons />
          </div>
        </div>
        <div
          v-else
          class="pl-2 w-96 h-16 mt-[-40px] ml-24 opacity-90 transition duration-150"
        >
          <img
            class="h-32 w-full"
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRHsS4Jpw5BsdDcw8pa7go7iqx1zrPzdc3Seg&usqp=CAU"
            alt=""
          />
        </div>
        <div
          class="ml-[120px] absolute mt-12 text-xs grid grid-cols-6 w-[330px]"
        >
          <p class="grid justify-center" :style="{ color: no2color }">
            <strong>{{ form.co }} </strong>
          </p>
          <p class="grid justify-center" :style="{ color: nh3color }">
            <strong>{{ form.nh3 }} </strong>
          </p>
          <p class="grid justify-center" :style="{ color: no2color }">
            <strong>{{ form.no }} </strong>
          </p>
          <p class="grid justify-center" :style="{ color: no2color }">
            <strong>{{ form.no2 }} </strong>
          </p>
          <p class="grid justify-center" :style="{ color: nh3color }">
            <strong>{{ form.o3 }} </strong>
          </p>
          <p class="grid justify-center">
            <strong>{{ form.so2 }} </strong>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ComponentsIcons from "./ComponentsIcons.vue";

export default {
  components: { ComponentsIcons },

  data() {
    return {
      errorMessage: "",
      q: "",
      lat: null,
      lon: null,
      cmponents: "",
      form: {
        name: "",
        country: "",
        lat: "",
        lon: "",
        temp: null,
        co: null,
        nh3: null,
        no: null,
        no2: null,
        o3: null,
        pm2_5: null,
        pm10: null,
        so2: null,
        flag: "",
      },
      nh3color: "",
      no2color: "",
      o3color: "",
    };
  },

  methods: {
    error() {
      if (this.q === "") {
        (this.errorMessage = "You have to type the name of city!"),
          setTimeout(() => {
            this.errorMessage = "";
          }, 3000);
      } else {
        axios
          .get(
            "http://api.openweathermap.org/geo/1.0/direct?q=" +
              this.q +
              "&limit=5&appid=992c20977dbb20bd9b6b36c9a376dc7c",
            null
          )
          .then((response) => {
            (this.q = ""), (this.zone = response);
            this.form.name = this.zone.data[0].name;
            this.form.lat = this.zone.data[0].lat;
            this.form.lon = this.zone.data[0].lon;
            axios
              .get(
                "https://api.openweathermap.org/data/2.5/weather?lat=" +
                  this.form.lat +
                  "&lon=" +
                  this.form.lon +
                  "&appid=992c20977dbb20bd9b6b36c9a376dc7c",
                null
              )
              .then((res) => {
                this.form.temp = res.data.main.temp - 273.15;
                this.form.temp = this.form.temp.toFixed(0);

                axios
                  .get(
                    "http://api.openweathermap.org/data/2.5/air_pollution/forecast?lat=" +
                      this.form.lat +
                      "&lon=" +
                      this.form.lon +
                      "&appid=992c20977dbb20bd9b6b36c9a376dc7c",
                    null
                  )
                  .then((response) => {
                    this.cmponents = response.data.list[1].components;
                    this.lat = null;
                    this.lon = null;
                    this.form.co = this.cmponents.co;
                    this.form.nh3 = this.cmponents.nh3;
                    this.form.no = this.cmponents.no;
                    this.form.no2 = this.cmponents.no2;
                    this.form.o3 = this.cmponents.o3;
                    this.form.pm2_5 = this.cmponents.pm2_5;
                    this.form.pm10 = this.cmponents.pm10;
                    this.form.so2 = this.cmponents.so2;
                    console.log("So2 is:" + this.form.so2);
                    localStorage.setItem("co", this.form.co);
                    localStorage.setItem("nh3", this.form.nh3);
                    localStorage.setItem("no", this.form.no);
                    localStorage.setItem("no2", this.form.no2);
                    localStorage.setItem("o3", this.form.o3);
                    localStorage.setItem("so2", this.form.so2);
                    localStorage.setItem("pm10", this.form.pm10);
                    localStorage.setItem("pm2_5", this.form.pm2_5);
                  });

                if (this.form.no2 < 60) {
                  this.no2color = "green";
                } else if (this.form.no2 > 60 && this.form.no2 < 120) {
                  this.no2color = "orange";
                } else if (this.form.no2 > 120 && this.form.no2 < 180) {
                  this.no2color = "red";
                } else if (this.form.no2 > 180 && this.form.no2 < 200) {
                  this.no2color = "darkred";
                } else if (this.form.no2 > 240) {
                  this.no2color = "brown";
                }

                if (this.form.o3 < 50) {
                  this.o3color = "green";
                } else if (this.form.o3 > 50 && this.form.o3 < 100) {
                  this.o3color = "orange";
                } else if (this.form.o3 > 100 && this.form.o3 < 200) {
                  this.o3color = "red";
                } else if (this.form.o3 > 200 && this.form.o3 < 400) {
                  this.o3color = "darkred";
                } else if (this.form.o3 > 400) {
                  this.o3color = "brown";
                }

                localStorage.setItem("name", this.form.name);
                localStorage.setItem("lat", this.form.lat);
                localStorage.setItem("lon", this.form.lon);
                localStorage.setItem("temp", this.form.temp);
              });
          });
      }
    },
  },
};
</script>
