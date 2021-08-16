<template>
  <div class="grid gap-4 md:grid-cols-2">
    <!-- Box 1 -->
    <div class="p-10 rounded bg-blue-100 shadow-md text-center">
      <h3 class="mb-4 text-3xl text-blue-900 font-bold">Cases</h3>
      <div class="mb-4 text-2xl">
        <span class="font-bold">New: </span
        >{{ numberWithCommas(stats.NewConfirmed) }}
      </div>
      <div class="mb-4 text-2xl">
        <span class="font-bold">Total: </span
        >{{ numberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- Box 2 -->
    <div class="p-10 rounded bg-blue-200 shadow-md text-center">
      <h3 class="mb-4 text-3xl text-blue-900 font-bold">Deaths</h3>
      <div class="mb-4 text-2xl">
        <span class="font-bold">New: </span
        >{{ numberWithCommas(stats.NewDeaths) }}
      </div>
      <div class="mb-4 text-2xl">
        <span class="font-bold">Total: </span
        >{{ numberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "DataBoxes",
  props: ["stats"],
  methods: {
    numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
  },
};
</script>
