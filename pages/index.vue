<template>
  <div class="index">
    <nav>
      <header @click="year++">▲</header>
      <section>{{year}}年</section>
      <footer @click="year--">▼</footer>
    </nav>
    <nav>
      <header @click="increment_month">▲</header>
      <section>{{month}}月</section>
      <footer @click="decrement_month">▼</footer>
    </nav>
    <Calendar :year="year" :month="month" v-model="schedules" />
  </div>
</template>

<script>
import Calendar from "~/components/Calendar.vue";
export default {
  components: {
    Calendar
  },
  data() {
    return {
      year: new Date().getFullYear(),
      month: new Date().getMonth() + 1,
      schedules: { "2020-07-11": "勉強会" }
    };
  },
  methods: {
    increment_month() {
      if (this.month < 12) {
        this.month++;
      } else {
        this.month = 1;
        this.year++;
      }
    },
    decrement_month() {
      if (this.month > 1) {
        this.month--;
      } else {
        this.month = 12;
        this.year--;
      }
    }
  },
  watch: {
    schedules: {
      deep: true,
      handler(value) {
        localStorage.schedules = JSON.stringify(value);
      }
    }
  },
  mounted() {
    if (localStorage.schedules) {
      try {
        this.schedules = JSON.parse(localStorage.schedules);
      } catch(e) {
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.index {
  display: flex;
  padding: 2em;
  > nav {
    display: flex;
    flex-direction: column;
    > header {
      font-size: 150%;
      cursor: pointer;
      text-align: center;
    }
    > footer {
      font-size: 150%;
      cursor: pointer;
      text-align: center;
    }
  }
}
</style>
