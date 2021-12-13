<template>
  <div class="about">
    <h1>{{ message }}</h1>
    <p>
      This program will prompt you to input the relevent data needed for a calculation. Not all possible fields are
      implemented yet.
    </p>
  </div>
</template>

<script>
// import axios from "axios";
export default {
  data: function () {
    return {
      message: "About",
    };
  },
  created: function () {},
  methods: {},
  setup() {},
};
</script>
