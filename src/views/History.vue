<template>
  <div class="history">
    <body>
      <h1>{{ message }}</h1>
      <div v-for="calc in calculations" :key="calc.id">
        <h3>{{ getChampName(calc.champion_id_one) }} attacking {{ getChampName(calc.champion_id_two) }}</h3>
        <p>Calculation id number: {{ calc.id }}</p>
        <p>{{ getChampName(calc.champion_id_one) }} level: {{ calc.champ_one_level }}</p>
        <p>{{ getChampName(calc.champion_id_two) }} level: {{ calc.champ_two_level }}</p>
        <p>
          {{ getChampName(calc.champion_id_two) }}'s hp before calculation: {{ calc.defending_champion_current_hp }}
        </p>
        <p>Ability: {{ getAbilityName(calc.ability_id) }}</p>
        <p>Ability Level: {{ calc.ability_level }}</p>
        <p>
          <b>{{ getChampName(calc.champion_id_one) }}'s items:</b>
        </p>
        <!-- attacking items -->
        <div v-if="calc.attacking_item_id_one">
          <p>{{ getItemName(calc.attacking_item_id_one) }}</p>
        </div>
        <div v-if="calc.attacking_item_id_two">
          <p>{{ getItemName(calc.attacking_item_id_two) }}</p>
        </div>
        <div v-if="calc.attacking_item_id_three">
          <p>{{ getItemName(calc.attacking_item_id_three) }}</p>
        </div>
        <div v-if="calc.attacking_item_id_four">
          <p>{{ getItemName(calc.attacking_item_id_four) }}</p>
        </div>
        <div v-if="calc.attacking_item_id_five">
          <p>{{ getItemName(calc.attacking_item_id_five) }}</p>
        </div>
        <div v-if="calc.attacking_item_id_six">
          <p>{{ getItemName(calc.attacking_item_id_six) }}</p>
        </div>
        <p>
          <b>{{ getChampName(calc.champion_id_two) }}'s items:</b>
        </p>
        <!-- defending items -->
        <div v-if="calc.defending_item_id_one">
          <p>{{ getItemName(calc.defending_item_id_one) }}</p>
        </div>
        <div v-if="calc.defending_item_id_two">
          <p>{{ getItemName(calc.defending_item_id_two) }}</p>
        </div>
        <div v-if="calc.defending_item_id_three">
          <p>{{ getItemName(calc.defending_item_id_three) }}</p>
        </div>
        <div v-if="calc.defending_item_id_four">
          <p>{{ getItemName(calc.defending_item_id_four) }}</p>
        </div>
        <div v-if="calc.defending_item_id_five">
          <p>{{ getItemName(calc.defending_item_id_five) }}</p>
        </div>
        <div v-if="calc.defending_item_id_six">
          <p>{{ getItemName(calc.defending_item_id_six) }}</p>
        </div>
        <p>Result: {{ calc.output }}</p>
        <button>this will eventually route to new calc with this as a starting point</button>
        <button>this will eventually delete the calc</button>
      </div>
    </body>
  </div>
</template>

<style scoped>
body {
  padding-top: 50px;
  padding: 100px;
}
h3 {
  padding-top: 50px;
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
      message: "History",
      calculations: [],
      champions: [], // used to replace id's in calc with the actual champions names
      abilities: [],
      items: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/calculations").then((response) => {
      this.calculations = response.data;
      console.log(response);
    });
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
    getChampName: function (calc_id) {
      let championId = this.champions.findIndex(function (champ) {
        return champ.id == calc_id;
      });
      let championName = this.champions[championId].name;
      return championName;
    },
    getAbilityName: function (calc_id) {
      let abilityId = this.abilities.findIndex(function (ability) {
        return ability.id == calc_id;
      });
      let abilityName = this.abilities[abilityId].name;
      return abilityName;
    },
    getItemName: function (calc_id) {
      let itemId = this.items.findIndex(function (item) {
        return item.id == calc_id;
      });
      let itemName = this.items[itemId].name;
      return itemName;
    },
  },
};
</script>
