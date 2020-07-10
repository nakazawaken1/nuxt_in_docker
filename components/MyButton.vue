<template>
  <a class="MyButton" :style="{'background-color': back_color, color: fore_color}">ボタン</a>
</template>

<script>
export default {
  props: {
    back_color: {
      type: String,
      default: "#00a656"
    },
    fore_color: {
      type: String,
      default: "#ffffff"
    }
  }
};
</script>

<style>
.MyButton {
  border-radius: 1.5em;
  box-shadow: 0 0.2em 0.5em rgba(0, 0, 0, 0.2);
  padding: 1em 2em;
  font-weight: bold;
  text-decoration: none;
}
</style>