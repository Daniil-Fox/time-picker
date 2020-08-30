<template>
  <section style="root">
    <div class="select" :style="{ width: this.width }">
      <p class="placeholder">{{ this.value }}</p>
      <button class="btn-time" @click="clickHandler">
        <img src="../assets/timer.svg" width="3rem" class="btn-picture" />
      </button>
    </div>
    <div class="clock-wrapper" :class="{ active }">
      <div class="clock" :style="{ 'background-color': this.backgroundColor }">
        <div class="clock-theme">
          <div class="container" v-for="idx in 12" :key="idx">
            <div class="block" :style="{ transform: `rotate(${idx * 30}deg)` }">
              <button
                v-if="layoutFromOne"
                class="square"
                :style="{ transform: `rotate(${270 - idx * 30}deg)` }"
                @click="selectHour(idx)"
              >
                {{ idx }}
              </button>
              <button
                v-else
                class="square"
                :style="{ transform: `rotate(${270 - idx * 30}deg)` }"
                @click="selectHour(idx + 12)"
              >
                {{ idx + 12 }}
              </button>
            </div>
          </div>
        </div>
      </div>
      <button class="btn-next" @click="nextHourLayout">
        <img src="../assets/next.svg" width="2rem" class="btn-picture" />
      </button>
    </div>
  </section>
</template>
<script>
export default {
  props: {
    backgroundColor: { type: String } || "E5E5E5",
    width: String,
    value: { type: Date || String } || new Date()
  },
  data: () => ({
    active: false,
    hour: Number,
    layoutFromOne: true
  }),
  methods: {
    clickHandler() {
      console.log(this.backgroundColor);
      this.active = !this.active;
    },
    selectHour(idx) {
      this.hour = idx;
      console.log(this.hour);
    },
    nextHourLayout() {
      this.layoutFromOne = !this.layoutFromOne;
    }
  },
  computed: {
    formatDate: () => {
      if (this.date) {
        console.log(this.date);
        if (typeof this.date === Date) {
          return `${this.date.getHours()}:${this.date.getMinutes()}:${this.date.getSeconds()}`;
        }
        return this.date;
      }
      return new Date();
    }
  }
};
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
}
.select {
  position: relative;
  border: none;
  background: #ececec;
  border-radius: 50px 50px 50px 50px;
  width: 40vh;
  height: 2.2rem;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
}
.block {
  width: 150px;

  height: 50px;
  display: flex;
  justify-content: start;
  align-items: center;
  transform-origin: 100%;
  position: absolute;
  bottom: -1.5rem;
}
.container {
  justify-content: start;
  align-items: center;
  transform: rotate(90deg);
  transform-origin: 100%;
  position: absolute;
}
.root {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.square {
  border: 1px solid black;
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.select::before {
  color: #868686;
  position: absolute;
  text-transform: uppercase;
  padding: 5px;
}
.btn-picture {
  width: 1.8rem;
  height: inherit;
  margin: 0.2rem 0.2rem;
}
.btn-time {
  border: 0px;
  background: none;
  outline: none;
  position: absolute;
  right: 0;
  width: 2.5rem;
}
.placeholder {
  position: absolute;
  display: none;
}
.clock-wrapper {
  margin: 2rem auto;
  border: 10px solid #ccc;
  width: 300px;
  height: 300px;
  border-radius: 100%;
  z-index: 100;
  display: none;
  text-align: center;
}
.active {
  display: block;
}
.clock {
  position: relative;
  z-index: 10;
  width: inherit;
  height: inherit;
  border-radius: inherit;
  background-size: 300px;
}
.clock-theme {
  background-image: url(../assets/dial.png);
  position: relative;
  width: inherit;
  height: inherit;
  background-size: 300px;
  display: flex;
  justify-content: center;
}
.btn-next {
  margin-top: 2rem;
}
</style>
