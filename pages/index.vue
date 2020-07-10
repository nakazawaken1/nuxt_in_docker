<template>
  <div class="container">
    <div>
      <MyButton/>
      <MyButton back_color="#666666"/>
      <MyButton back_color="#330000" fore_color="#ffeeee"/>
    </div>
  </div>
</template>

<script>
import MyButton from "~/components/MyButton.vue";
export default {
  components: {
    MyButton
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
