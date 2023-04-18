<template>
  <v-container>
    <v-row>
      <v-col
        v-for="(car, index) in filteredCars"
        :key="index"
        cols="12"
        md="6"
        lg="4"
      >
        <v-card>
          <v-img :src="car.image" height="200px" contain></v-img>
          <v-card-title>
            <div class="headline mb-0">{{ car.Company }} {{ car.model }}</div> &nbsp; &nbsp;
            <div class="grey--text">{{ car.year }}</div>
          </v-card-title>
          <v-card-text>
            <div class="headline mb-0"> ₹ {{ car.price }}</div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>

    <v-divider></v-divider>

    <v-row>
      <v-col cols="12" md="4" lg="3">
        <v-select v-model="selectedYear" :items="years" label="Year"></v-select>
      </v-col>
      <v-col cols="12" md="4" lg="3">
        <v-select v-model="selectedCompany" :items="Companys" label="Make"></v-select>
      </v-col>
      <v-col cols="12" md="4" lg="3">
        <v-select
          v-model="selectedModel"
          :items="models"
          label="Model"
        ></v-select>
      </v-col>
      <v-col cols="12" md="4" lg="3">
        <v-select
          v-model="selectedPrice"
          :items="prices"
          label="Price"
        ></v-select>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import cars from "../assets/cars.json"

export default {
  data() {
    return {
      selectedYear: null,
      selectedCompany: null,
      selectedModel: null,
      selectedPrice: null,
      years: [],
      Companys: [],
      models: [],
      prices: [],
    };
  },
  computed: {
    filteredCars() {
      let filteredCars = cars.slice();

      if (this.selectedYear) {
        filteredCars = filteredCars.filter(
          (car) => car.year === this.selectedYear
        );
      }

      if (this.selectedCompany) {
        filteredCars = filteredCars.filter(
          (car) => car.Company === this.selectedCompany
        );
      }

      if (this.selectedModel) {
        filteredCars = filteredCars.filter(
          (car) => car.model === this.selectedModel
        );
      }

      if (this.selectedPrice) {
        filteredCars = filteredCars.filter(
          (car) => car.price === this.selectedPrice
        );
      }

      return filteredCars.slice(0, 24);
    },
  },
  mounted() {
    this.years = [...new Set(cars.map((car) => car.year))];
    this.Companys = [...new Set(cars.map((car) => car.Company))];
    this.models = [...new Set(cars.map((car) => car.model))];
    this.prices = [...new Set(cars.map((car) => car.price))];
  },
};
</script>

<style>
</style>

