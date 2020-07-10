<template>
  <div class="container">
    <div>
      <MyButton />
      <MyButton back_color="#666666" />
      <MyButton back_color="#330000" fore_color="#ffeeee" />
      <MyButton left_arrow />
      <MyButton right_arrow />
      <MyButton left_arrow right_arrow />
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
