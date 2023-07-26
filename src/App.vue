<template>
  <Button />
  <div class="container">
    <div class="header">
      <p></p>
    </div>
    <div class="center">
      <p></p>
    </div>
    <div class="bottom">
      <div>
        <p></p>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button.vue";

export default {
  name: "App",
  components: {
    Button,
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
  }
  .bottom {
    grid-area: bottom;
    display: grid;
    grid-template-rows: repeat(1, 1fr);
    gap: 10px;
  }
}
</style>
