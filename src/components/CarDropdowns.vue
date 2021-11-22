<template>
  <div class="space-x-12">
    <DropDown :items="yearList" v-on:selected="selectedYear" />
    <DropDown :items="makeList" v-on:selected="selectedMake" />
    <DropDown :items="modelList" />
  </div>
</template>

<script>
import DropDown from "./DropDown.vue";

export default {
  components: {
    DropDown,
  },
  data() {
    return {
      yearList: [],
      makeList: [],
      modelList: [],
      currentYear: "",
      currentMake: "",
    };
  },
  methods: {
    getYear() {
      this.axios
        .get(
          "https://rateengine.ship.cars/v2/vehicles/years/?token=5cbe12fb62f4941267d623499a2a4fd5948fd3ef"
        )
        .then((res) => {
          this.yearList = res.data.map((item) => item.year);
        });
    },
    selectedYear(value) {
      this.currentYear = value;
      this.axios
        .get(
          `https://rateengine.ship.cars/v2/vehicles/makes/?year=${value}&token=5cbe12fb62f4941267d623499a2a4fd5948fd3ef`
        )
        .then((res) => {
          this.makeList = res.data.map((item) => item.make);
        });
    },
    selectedMake(value) {
      this.currentMake = value;
      this.axios
        .get(
          `https://rateengine.ship.cars/v2/vehicles/models/?year=${this.currentYear}&make=${value}&token=5cbe12fb62f4941267d623499a2a4fd5948fd3ef`
        )
        .then((res) => {
          console.log(res.data);
          this.modelList = res.data.map((item) => item.model);
        });
    },
  },
  mounted() {
    this.getYear();
  },
};
</script>

<style scoped>
</style>
