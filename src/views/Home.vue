<template>
  <div class="home">
    <body>
      <h1>{{ message }}</h1>
      <!-- <p>{{ champions }}</p> -->
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
            <!-- datalist for items -->
            <datalist id="items">
              <option v-for="item in items" :key="item.id">
                {{ item.name }}
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
          </div>
          <!-- row 5 -->
          <div class="row">
            <div class="col-md-3">
              <label for="item1">Choose an item:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="attackingItemOne" list="items" />
            </div>
            <div class="col-md-3">
              <label for="item1">Choose an item:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="defendingItemOne" list="items" />
            </div>
          </div>
          <!-- row 6 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemOne">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemOne">
              <input type="text" v-model="attackingItemTwo" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemOne">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemOne">
              <input type="text" v-model="defendingItemTwo" list="items" />
            </div>
          </div>
          <!-- row 7 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemTwo">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemTwo">
              <input type="text" v-model="attackingItemThree" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemTwo">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemTwo">
              <input type="text" v-model="defendingItemThree" list="items" />
            </div>
          </div>
          <!-- row 8 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemThree">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemThree">
              <input type="text" v-model="attackingItemFour" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemThree">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemThree">
              <input type="text" v-model="defendingItemFour" list="items" />
            </div>
          </div>
          <!-- row 9 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemFour">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemFour">
              <input type="text" v-model="attackingItemFive" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemFour">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemFour">
              <input type="text" v-model="defendingItemFive" list="items" />
            </div>
          </div>
          <!-- row 10 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemFive">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemFive">
              <input type="text" v-model="attackingItemSix" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemFive">
              <label for="item1">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemFive">
              <input type="text" v-model="defendingItemSix" list="items" />
            </div>
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
          <div class="row" v-if="output">
            <div class="col-md-6 .offset-3">Calculation details: {{ output }}</div>
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
      items: [],
      currentCalculation: {
        champion_id_one: null,
        champion_id_two: null,
        ability_id: null,
        output: null,
        champ_one_level: null,
        champ_two_level: null,
        ability_level: null,
        defending_champion_current_hp: null,
      },
      championOneName: "",
      championTwoName: "",
      abilityName: "",
      attackingItemOne: "",
      defendingItemOne: "",
      attackingItemTwo: "",
      defendingItemTwo: "",
      attackingItemThree: "",
      defendingItemThree: "",
      attackingItemFour: "",
      defendingItemFour: "",
      attackingItemFive: "",
      defendingItemFive: "",
      attackingItemSix: "",
      defendingItemSix: "",
      output: null,
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
    axios.get("http://localhost:3000/items").then((response) => {
      this.items = response.data;
      console.log(this.items);
    });
  },
  methods: {
    // fields of currentCalculation need to be translated from newThing to id first
    createCalculation(currentCalculation, championOneName, championTwoName, abilityName) {
      currentCalculation.champion_id_one = this.champions.find((champ) => champ.name === championOneName).id;
      currentCalculation.champion_id_two = this.champions.find((champ) => champ.name === championTwoName).id;
      currentCalculation.ability_id = this.abilities.find((ability) => ability.name === abilityName).id;
      currentCalculation.attacking_item_id_one = this.items.find((item) => item.name === this.attackingItemOne).id;
      currentCalculation.attacking_item_id_two = this.items.find((item) => item.name === this.attackingItemTwo).id;
      currentCalculation.attacking_item_id_three = this.items.find((item) => item.name === this.attackingItemThree).id;
      currentCalculation.attacking_item_id_four = this.items.find((item) => item.name === this.attackingItemFour).id;
      currentCalculation.attacking_item_id_five = this.items.find((item) => item.name === this.attackingItemFive).id;
      currentCalculation.attacking_item_id_six = this.items.find((item) => item.name === this.attackingItemSix).id;
      currentCalculation.defending_item_id_one = this.items.find((item) => item.name === this.defendingItemOne).id;
      currentCalculation.defending_item_id_two = this.items.find((item) => item.name === this.defendingItemTwo).id;
      currentCalculation.defending_item_id_three = this.items.find((item) => item.name === this.defendingItemThree).id;
      currentCalculation.defending_item_id_four = this.items.find((item) => item.name === this.defendingItemFour).id;
      currentCalculation.defending_item_id_five = this.items.find((item) => item.name === this.defendingItemFive).id;
      currentCalculation.defending_item_id_six = this.items.find((item) => item.name === this.defendingItemSix).id;
      console.log("this is the thing", this.currentCalculation);
      axios.post("http://localhost:3000/calculations", currentCalculation).then((response) => {
        console.log(response.data);
        this.output = response.data.output;
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
