<template>
  <Button />
  <div class="container">
    <div class="header" :style="{ backgroundColor: data[randomNumber].color }">
      <p>{{ data[randomNumber].name }}</p>
    </div>
    <div class="center">
      <p>
        {{ convertDate(data[randomNumber].from) }} -
        {{ convertDate(data[randomNumber].to) }}
      </p>
    </div>
    <div class="bottom" :style="gridStyle">
      <div
        v-for="(item, index) in data[randomNumber].talent"
        :key="index"
        :style="{
          backgroundColor: data[randomNumber].color,
        }"
        class="box"
      >
        <p>
          {{ item }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button.vue";
import data from "./config/data.json";

export default {
  name: "App",
  components: {
    Button,
  },
  data() {
    return {
      data: data,
      randomNumber: 1,
    };
  },
  computed: {
    gridStyle() {
      return {
        // A dinamikusság miatt visszadja, hogy hány oszlopot kell majd generálni.
        gridTemplateColumns: `repeat(${
          this.data[this.randomNumber].talent.length
        }, 1fr)`,
      };
    },
  },
  methods: {
    convertDate: (oldDate) => {
      //Konvertálja a dátumot hónap, napra
      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      const date = new Date(oldDate);

      const monthIndex = date.getMonth();
      const day = date.getDate();

      return `${months[monthIndex]} ${day}`;
    },
  },
};
</script>

<style lang="scss">
.container {
  width: 800px;
  height: 300px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 110px 60px 110px;
  gap: 10px;
  row-gap: 10px;
  padding: 10px;
  grid-template-areas:
    "header header header"
    "center center center"
    "bottom bottom bottom";

  .header {
    grid-area: header;
  }
  .center {
    grid-area: center;
    background-color: white;
  }
  .bottom {
    grid-area: bottom;
    display: grid;
    grid-template-rows: repeat(1, 1fr);
    gap: 10px;
  }
}
</style>
