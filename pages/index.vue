<template>
  <div class="container">
    <ul>
      <li>
        <label>身長</label>
        <input type="nubmer" v-model="tall" />
        <span>cm</span>
      </li>
      <li>
        <label>体重</label>
        <input type="nubmer" v-model="weight" />
        <span>kg</span>
      </li>
      <li>BMI(Body Mass Index) = {{format(bmi)}}</li>
      <li>適正体重 = {{format(standard_weight)}}kg</li>
      <li>適正体重との差 = {{format(weight - standard_weight)}}kg</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tall: 185,
      weight: 80
    };
  },
  computed: {
    bmi() {
      return (this.weight / (this.tall * this.tall)) * 10000;
    },
    standard_weight() {
      return (this.tall * this.tall * 22) / 10000;
    }
  },
  methods: {
    format(value) {
      const x100 = value * 100;
      return Math.round(x100) / 100;
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  > ul {
    list-style-type: none;
    > li {
      margin: 1em;
    }
  }
}
</style>
