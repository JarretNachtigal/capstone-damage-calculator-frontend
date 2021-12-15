<template>
  <div class="home">
    <body>
      <h1>{{ message }}</h1>
      <!-- champions dropdown-->
      <div>
        <form v-on:submit.prevent="createCalculation(currentCalculation)">
          <div class="row">
            <div class="col-md-5 offset-md-1">
              <label for="champions">Choose an attacking champion:</label>
              <input type="text" v-model="currentCalculation.champion_id_one" list="champions" />
            </div>
            <div class="col-md-5 offset-md-1">
              <label for="champions">Choose a defending champion:</label>
              <input type="text" v-model="currentCalculation.champion_id_two" list="champions" />
            </div>
            <!-- datalist for champion input -->
            <datalist id="champions">
              <option v-for="champ in champions" :key="champ.id">
                {{ getChampName(champ.id) }}
              </option>
            </datalist>
          </div>
          <div class="row">
            <div class="col-sm-4 offset-5">
              <input type="submit" />
            </div>
          </div>
        </form>
      </div>
    </body>
  </div>
</template>

<style scoped>
body {
  padding: 100px;
}
h1 {
  text-align: center;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Home",
      champions: [],
      abilities: [],
      currentCalculation: {},
      championNames: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/champions").then((response) => {
      this.champions = response.data;
      console.log(this.champions);
    });
    axios.get("http://localhost:3000/abilities").then((response) => {
      this.abilities = response.data;
      console.log(this.abilities);
    });
    // this.championNames = this.champions.map(); // make a hash with :name and :id
  },
  methods: {
    createCalculation() {
      axios.post("http://localhost:3000/calculations", this.currentCalculation).then((response) => {
        console.log(response.data);
      });
    },
    getChampName: function (calc_id) {
      let championId = this.champions.findIndex(function (champ) {
        return champ.id == calc_id;
      });
      let championName = this.champions[championId].name;
      return championName;
    },
  },
};
</script>
