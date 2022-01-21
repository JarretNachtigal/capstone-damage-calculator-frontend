<template>
  <div class="home">
    <body>
      <h1>{{ title }}</h1>
      <p>{{ champions }}</p>
      <p>{{ abilities }}</p>
      <p>{{ items }}</p>
      <!-- champions dropdown-->
      <div>
        <form>
          <!-- row 1 -->
          <div class="row">
            <!-- datalist for champions -->
            <datalist id="champions">
              <option v-for="champ in champions" :key="champ.id">
                {{ champ.name }}
              </option>
            </datalist>
            <!-- datalist for abilities -->
            <datalist id="abilities">
              <option v-for="ability in abilities" :key="ability.id">
                {{ ability.name }}
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
              <input type="text" v-model="championsV2[0].name" list="champions" />
            </div>
            <div class="col-md-3">
              <label for="champions">Choose a defending champion:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="championsV2[1].name" list="champions" />
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
              <input type="text" v-model="abilitiesV2.name" list="abilities" />
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
              <input type="text" v-model="attackingItemsV2[0].name" list="items" />
            </div>
            <div class="col-md-3">
              <label for="item2">Choose an item:</label>
            </div>
            <div class="col-md-3">
              <input type="text" v-model="defendingItemsV2[0].name" list="items" />
            </div>
          </div>
          <!-- row 6 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemsV2[0].name">
              <label for="item3">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemsV2[0].name">
              <input type="text" v-model="attackingItemsV2[1].name" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[0].name">
              <label for="item4">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[0].name">
              <input type="text" v-model="defendingItemsV2[1].name" list="items" />
            </div>
          </div>
          <!-- row 7 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemsV2[1].name">
              <label for="item5">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemsV2[1].name">
              <input type="text" v-model="attackingItemsV2[2].name" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[1].name">
              <label for="item6">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[1].name">
              <input type="text" v-model="defendingItemsV2[2].name" list="items" />
            </div>
          </div>
          <!-- row 8 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemsV2[2].name">
              <label for="item7">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemsV2[2].name">
              <input type="text" v-model="attackingItemsV2[3].name" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[2].name">
              <label for="item8">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[2].name">
              <input type="text" v-model="defendingItemsV2[3].name" list="items" />
            </div>
          </div>
          <!-- row 9 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemsV2[3].name">
              <label for="item9">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemsV2[3].name">
              <input type="text" v-model="attackingItemsV2[4].name" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[3].name">
              <label for="item10">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[3].name">
              <input type="text" v-model="defendingItemsV2[4].name" list="items" />
            </div>
          </div>
          <!-- row 10 -->
          <div class="row">
            <div class="col-md-3" v-if="attackingItemsV2[4].name">
              <label for="item11">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="attackingItemsV2[4].name">
              <input type="text" v-model="attackingItemsV2[5].name" list="items" />
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[4].name">
              <label for="item12">Choose another item:</label>
            </div>
            <div class="col-md-3" v-if="defendingItemsV2[4].name">
              <input type="text" v-model="defendingItemsV2[5].name" list="items" />
            </div>
          </div>
          <!-- submit button row -->
          <div class="row">
            <div class="col-sm-6">
              <button type="button" v-on:click="createCalculation()">submit</button>
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
      title: "New Calculation",
      // these hold the data from the backend, not the user selected champions and abilities
      champions: [],
      abilities: [],
      items: [],
      // this is the object that will be sent to the backend to do the calculation
      currentCalculation: {
        champion_id_one: null,
        champion_id_two: null,
        ability_id: null,
        output: null,
        champ_one_level: null,
        champ_two_level: null,
        ability_level: null,
        defending_champion_current_hp: null,
        attacking_item_id_one: null,
        attacking_item_id_two: null,
        attacking_item_id_three: null,
        attacking_item_id_four: null,
        attacking_item_id_five: null,
        attacking_item_id_six: null,
        defending_item_id_one: null,
        defending_item_id_two: null,
        defending_item_id_three: null,
        defending_item_id_four: null,
        defending_item_id_five: null,
        defending_item_id_six: null,
      },
      // new
      // first champion is attacking, second is defending
      championsV2: [
        { name: null, id: null },
        { name: null, id: null },
      ],
      // abilities array, will hold abilities of current selected attacking champion
      abilitiesV2: [{ name: null, id: null }], // eventually hold more than one and do multiple calcs
      // attacking items array, holds up to six selected items
      attackingItemsV2: [
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
      ],
      // defending items array
      defendingItemsV2: [
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
        { name: null, id: null },
      ],
      output: null,
    };
  },
  created: function () {
    axios.get("http://localhost:3000/champions").then((response) => {
      response.data.map((champion) => {
        this.champions.push({ name: champion.name, id: champion.id });
      });
    });
    axios.get("http://localhost:3000/abilities").then((response) => {
      response.data.map((ability) => {
        this.abilities.push({ name: ability.name, id: ability.id });
      });
    });
    axios.get("http://localhost:3000/items").then((response) => {
      response.data.map((item) => {
        this.items.push({ name: item.name, id: item.id });
      });
    });
  },
  methods: {
    // these are broken
    setItemIds() {
      console.log("inside setItemIds");
      this.attackingItemsV2.map((item) => (item.id = this.items.find((i) => (item.name = i.name).id)));
      this.defendingItemsV2.map((item) => (item.id = this.items.find((i) => (item.name = i.name).id)));
    },
    setChampionIds() {
      console.log("inside setChampionIds");
      this.championsV2[0].id = this.champions.find((champ) => champ.name === this.championsV2[0].name).id;
      this.championsV2[1].id = this.champions.find((champ) => champ.name === this.championsV2[1].name).id;
    },
    setAbilityIds() {
      console.log("inside setAbilityIds");
      this.abilitiesV2.map((ability) => (ability.id = this.abilities.find((a) => (ability.name = a.name).id)));
    },
    // fields of currentCalculation need to be translated from newThing to id first
    createCalculation() {
      this.currentCalculation.output = null;
      // set ids from names
      this.setChampionIds();
      this.setAbilityIds();
      this.setItemIds();
      // get champion id's from champion names
      this.currentCalculation.champion_id_one = this.champions.find(
        (champ) => champ.name === this.championsV2[0].name
      ).id;
      this.currentCalculation.champion_id_two = this.champions.find(
        (champ) => champ.name === this.championsV2[1].name
      ).id;
      // get ability id's from ability names
      this.currentCalculation.ability_id = this.abilities.find(
        (ability) => ability.name === this.abilitiesV2[0].name
      ).id;

      //items array into currentCalculation object
      this.currentCalculation.attacking_item_id_one = this.attackingItemsV2[0].id;
      this.currentCalculation.attacking_item_id_two = this.attackingItemsV2[1].id;
      this.currentCalculation.attacking_item_id_three = this.attackingItemsV2[2].id;
      this.currentCalculation.attacking_item_id_four = this.attackingItemsV2[3].id;
      this.currentCalculation.attacking_item_id_five = this.attackingItemsV2[4].id;
      this.currentCalculation.attacking_item_id_six = this.attackingItemsV2[5].id;

      this.currentCalculation.defending_item_id_one = this.defendingItemsV2[0].id;
      this.currentCalculation.defending_item_id_two = this.defendingItemsV2[1].id;
      this.currentCalculation.defending_item_id_three = this.defendingItemsV2[2].id;
      this.currentCalculation.defending_item_id_four = this.defendingItemsV2[3].id;
      this.currentCalculation.defending_item_id_five = this.defendingItemsV2[4].id;
      this.currentCalculation.defending_item_id_six = this.defendingItemsV2[5].id;

      console.log("this is the thing", this.currentCalculation);
      axios.post("http://localhost:3000/calculations", this.currentCalculation).then((response) => {
        console.log(response.data);
        this.output = response.data.output;
      });
    },
    // this will get called when an attacking champion is selected eventually
    getAbilities(champ_id) {
      this.abilities = this.champions;
      console.log(champ_id);
    },
  },
};
</script>
