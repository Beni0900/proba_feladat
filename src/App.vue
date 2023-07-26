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
          ...(index === 0 ? { borderBottomLeftRadius: '15px' } : {}),
          ...(index === data[randomNumber].talent.length - 1
            ? { borderBottomRightRadius: '15px' }
            : {}),
        }"
        class="box"
      >
        <p
          :style="{
            ...(index === data[randomNumber].talent.length - 1
              ? { textAlign: 'right' }
              : {}),
            ...(index === 0 ? { textAlign: 'left' } : {}),
          }"
        >
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
@mixin flex-center {
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  border: 4px solid white;
  border-radius: 20px;
  width: 790px;
  height: 290px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: 110px 50px 110px;
  gap: 5px;
  row-gap: 9px;
  padding: 9px;
  grid-template-areas:
    "header header header"
    "center center center"
    "bottom bottom bottom";

  .header {
    grid-area: header;
    @include flex-center();
    border-radius: 15px 15px 0 0;
    p {
      font-weight: 700;
      transform: scaleY(1.3);
      text-transform: uppercase;
    }
  }
  .center {
    grid-area: center;
    background-color: white;
    @include flex-center();
    p {
      color: black;
      text-shadow: none;
      font-size: 20px;
      transform: scaleY(1.1);
    }
  }
  .bottom {
    grid-area: bottom;
    display: grid;
    grid-template-rows: repeat(1, 1fr);
    gap: 7px;
    .box {
      display: flex;
      justify-content: center;
      align-items: center;
      p {
        transform: scaleY(1.2);
        font-weight: 400;
      }
    }
  }
  p {
    width: 70%;
    text-align: center;
    margin: 0;
    color: white;
    font-size: 30px;
    text-shadow: 2px 2px 0px #000000;
    line-height: 25px;
  }
}
</style>
