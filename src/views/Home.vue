<template>
  <div class="home">
    <body>
      <h1>{{ message }}</h1>
      <!-- <h1>{{ abilities }}</h1> -->
      <!-- champions dropdown-->
      <div>
        <form>
          <!-- row 1 -->
          <div class="row">
            <!-- datalist for champions -->
            <datalist id="champions">
              <option v-for="champ in champions" :key="champ.id">
                {{ getChampName(champ.id) }}
              </option>
            </datalist>
            <!-- datalist for abilities -->
            <datalist id="abilities">
              <option v-for="ability in abilities" :key="ability.id">
                {{ getAbilityName(ability.id) }}
              </option>
            </datalist>
            <!-- datalist for champion levels -->
            <datalist id="levels">
              <option v-for="index in 18" :key="index">
                {{ index }}
              </option>
            </datalist>
            <!-- datalist for ability levels -->
            <datalist id="ability levels">
              <option v-for="index in 5" :key="index">
                {{ index }}
              </option>
            </datalist>
            <div class="col-md-3">
              <label for="champions">Choose an attacking champion:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="championOneName" list="champions" />
            </div>
            <div class="col-md-3">
              <label for="champions">Choose a defending champion:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="championTwoName" list="champions" />
            </div>
          </div>
          <!-- row 2 -->
          <div class="row">
            <div class="col-md-3">
              <label for="levelsone">Attacking champion level:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="currentCalculation.champ_one_level" list="levels" />
            </div>
            <div class="col-md-3">
              <label for="levelstwo">Defending champion Level:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="currentCalculation.champ_two_level" list="levels" />
            </div>
          </div>
          <!-- row 3 -->
          <div class="row">
            <div class="col-md-3">
              <label for="abilities">Choose an ability:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="abilityName" list="abilities" />
            </div>
            <div class="col-md-3">
              <label for="defendinghp">Defending champion hp: (default full)</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="currentCalculation.defending_champion_current_hp" />
            </div>
          </div>
          <!-- row 4 -->
          <div class="row">
            <div class="col-md-3">
              <label for="ability levels">Ability level:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="currentCalculation.ability_level" list="ability levels" />
            </div>
            <!-- <div class="col-md-3">
              <label for="item2">Choose an item:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="defendingItemOne" list="items" />
            </div> -->
          </div>
          <!-- submit button row -->
          <div class="row">
            <div class="col-sm-6">
              <button
                type="button"
                v-on:click="createCalculation(currentCalculation, championOneName, championTwoName, abilityName)"
              >
                submit
              </button>
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
      message: "New Calculation",
      champions: [],
      abilities: [],
      currentCalculation: {},
      championNames: [],
      // used to hold info before translating names into ids and requesting new calculation from backend
      championOneName: "",
      championTwoName: "",
      abilityName: "",
      attackingItemOne: "",
      defendingItemOne: "",
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
  },
  methods: {
    // fields of currentCalculation need to be translated from newThing to id first
    createCalculation(currentCalculation, championOneName, championTwoName, abilityName) {
      currentCalculation.champion_id_one = this.champions.findIndex(function (champ) {
        if (champ.name === championOneName) {
          return champ.id;
        }
      });
      // this.currentCalculation.champion_id_one++;
      currentCalculation.champion_id_two = this.champions.findIndex(function (champ) {
        if (champ.name === championTwoName) {
          return champ.id;
        }
      });
      // this.currentCalculation.champion_id_two++;
      currentCalculation.ability_id = this.abilities.findIndex(function (ability) {
        if (ability.name === abilityName) {
          return ability.id;
        }
      });
      // this.currentCalculation.ability_id++;
      console.log("this is the thing", this.currentCalculation);
      axios.post("http://localhost:3000/calculations", currentCalculation).then((response) => {
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
    getAbilityName: function (calc_id) {
      let abilityId = this.abilities.findIndex(function (champ) {
        return champ.id == calc_id;
      });
      let abilityName = this.abilities[abilityId].name;
      return abilityName;
    },
    // this will get called when an attacking champion is selected
    getAbilities(champ_id) {
      this.abilities = this.champions;
      console.log(champ_id);
    },
  },
};
</script>
