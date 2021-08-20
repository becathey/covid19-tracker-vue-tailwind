<template>
  <main v-if="!loading" class="mb-5">
    <div class="flex flex-col sm:flex-row align-center justify-center mb-10">
      <CountrySelect @get-country="getCountryData" :countries="countries" />
      <button
        v-if="stats.Country"
        @click="clearCountryData"
        class="flex-initial rounded mt-2 p-3 bg-green-700 text-white focus:outline-none hover:bg-green-600"
      >
        Clear Country
      </button>
    </div>
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
  </main>
  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="mt-10 mb-6 text-3xl text-gray-500">Fetching Data</div>
    <img :src="loadingImage" class="w-24 m-auto" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";
import CountrySelect from "@/components/CountrySelect";
export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global";
      this.stats = data.Global;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
