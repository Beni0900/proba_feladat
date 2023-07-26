<template>
  <div class="buttonContainer">
    <button type="button">Overlay</button>
  </div>
</template>

<script>
export default {
  name: "Button",
};
</script>

<style lang="scss">
.buttonContainer {
  position: absolute;
  top: 30px;
  right: 20px;
  width: 10%;
  height: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
