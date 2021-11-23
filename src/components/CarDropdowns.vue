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
        .get("http://new.api.nexusautotransport.com/api/vehicles/years")
        .then((res) => {
          this.yearList = [...res.data.data];
        });
    },
    selectedYear(value) {
      this.currentYear = value;
      this.axios
        .get(
          `http://new.api.nexusautotransport.com/api/vehicles/makes/?year=${value}`
        )
        .then((res) => {
          this.makeList = res.data.data.map((item) => item.name);
        });
    },
    selectedMake(value) {
      this.currentMake = value;
      this.axios
        .get(
          `http://new.api.nexusautotransport.com/api/vehicles/?year=${this.currentYear}&make=${value}`
        )
        .then((res) => {
          this.modelList = res.data.data.map((item) => item.model);
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
