<template>
  <v-container class="text-center">
    <v-btn class="mt-4" rounded outlined v-on:click="get_from_server" :loading="loading">Refresh</v-btn>
    <v-divider class="mt-4"></v-divider>
    <div v-if="loading">
      <v-skeleton-loader boilerplate="false" type="article" tile="false" class="mx-auto"></v-skeleton-loader>
    </div>

    <div v-else>
      <p class="disp font-weight-bold mt-4">
        Data are as of:
        <span class="disp font-weight-regular">{{dateNoww}} GMT+3</span>
      </p>

      <h1 class="disp mt-3">
        <v-avatar size="70" class="mr-4">
          <v-img src="@/assets/ethiopia.png"></v-img>
        </v-avatar>
        {{res_data.country}}
      </h1>

      <p class="disp font-weight-bold mt-3">
        Total Cases :
        <span class="disp font-weight-regular">{{res_data.total_case}}</span>
      </p>
      <p class="disp font-weight-bold">
        New Cases (as of today ) :
        <span class="disp font-weight-regular">{{res_data.new_case}}</span>
      </p>
      <p class="disp font-weight-bold">
        Total Death Cases :
        <span class="disp font-weight-regular">{{res_data.total_death}}</span>
      </p>
      <p class="disp font-weight-bold">
        New Deaths (as of today) :
        <span class="disp font-weight-regular">{{res_data.new_death}}</span>
      </p>
      <p class="disp font-weight-bold">
        Total Recovered Cases :
        <span class="disp font-weight-regular">{{res_data.total_recovered}}</span>
      </p>
      <p class="disp font-weight-bold">
        Active Cases :
        <span class="disp font-weight-regular">{{res_data.active_case}}</span>
      </p>
      <p class="disp font-weight-bold">
        Serious Cases :
        <span class="disp font-weight-regular">{{res_data.serious_critical}}</span>
      </p>

      <p class="disp font-weight-bold">
        Total Cases out of 1 M pop :
        <span
          class="disp font-weight-regular"
        >{{res_data.total_cases_1_M_pop}}</span>
      </p>
      <v-divider></v-divider>
      <p class="disp font-weight-bold">
        <v-list rounded disabled>
          <v-list-item-group>
            <v-list-tile-title class="disp font-weight-thin">#NOTE</v-list-tile-title>
            <v-list-item>
              <v-list-item-content>
                <p>*Data is static and changed from time to time. Make sure you press the "Get Data" button regularly for updates</p>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </p>
    </div>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "MainPage",

  data: () => {
    return {
      res_data: {},
      loading: false,
      timeStamp: "",
      dialog: false
    };
  },
  created() {
    this.get_from_server();
    
  },
  methods: {
    async get_from_server() {
      
      this.loading = true;
      const res = await axios.get("https://coronavirus-scrapy.herokuapp.com/");
      
      this.dateNoww = new Date().toLocaleString()

      this.res_data = res.data;
      this.loading = false;
      
          
    },
    callFunction() {

      var currentDate = new Date();
      
      var test1 = currentDate.toLocaleString();

      this.dateNoww = test1;
    }
  },
  mounted() {
    this.callFunction();
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Poppins&display=swap");

.disp {
  font-family: "Poppins", sans-serif;
}
</style>