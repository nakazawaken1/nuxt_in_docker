<template>
  <div class="Calendar">
    <section v-for="day in days" :key="day" :class="'wday' + (day + wday_offset) % 7">
      <header>{{day}}({{wday(day)}})</header>
      <article @click="editing = format(day)">
        <nav v-if="editing == format(day)">
          <input v-model="value[format(day)]" @keyup.enter="editing = null" type="text" />
          <button @click.stop="editing = null">確定</button>
        </nav>
        <span v-else>
          <strong>{{holidays[year] && holidays[year][format(day)]}}</strong>
          &nbsp;
          {{value[format(day)]}}
        </span>
      </article>
    </section>
  </div>
</template>

<script>
export default {
  props: {
    year: {
      type: Number,
      default: new Date().getFullYear()
    },
    month: {
      type: Number,
      default: new Date().getMonth() + 1
    },
    value: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      editing: null,
      holidays: {} //{year:{date:name}}
    };
  },
  computed: {
    first_day() {
      return new Date(this.year, this.month - 1, 1);
    },
    last_day() {
      return new Date(this.year, this.month, 0);
    },
    wday_offset() {
      return this.first_day.getDay() - 1;
    },
    days() {
      return [...Array(this.last_day.getDate() - this.first_day.getDate())].map(
        (_, i) => i + 1
      );
    }
  },
  watch: {
    year: {
      immediate: true,
      async handler(value) {
        if (!(value in this.holidays)) {
          this.$set(
            this.holidays,
            value,
            await (
              await fetch(
                `https://holidays-jp.github.io/api/v1/${this.year}/date.json`
              )
            ).json()
          );
        }
      }
    }
  },
  methods: {
    wday(day) {
      return "日月火水木金土".charAt((day + this.wday_offset) % 7);
    },
    format(day) {
      return `${this.year}-${("0" + this.month).slice(-2)}-${("0" + day).slice(
        -2
      )}`;
    }
  }
};
</script>

<style lang="scss" scoped>
.Calendar {
  margin-left: 1em;
  border: 1px solid #dddddd;
  > section {
    display: flex;
    align-items: center;
    ~ section {
      border-top: 1px solid #dddddd;
    }
    &:hover {
      background-color: #ffff99;
    }
    &.wday0 {
      > header {
        color: red;
      }
    }
    &.wday6 {
      > header {
        color: blue;
      }
    }
    > header {
      border-right: 1px solid #dddddd;
      flex: 0 0 4em;
      padding: 0.1em 0.5em;
      text-align: right;
    }
    > article {
      width: 50vw;
      padding: 0.1em 0.5em;
      cursor: pointer;
      > nav {
        display: flex;
        > input {
          flex: 1 0 auto;
        }
      }
      > span {
        > strong {
          color: pink;
        }
      }
    }
  }
}
</style>