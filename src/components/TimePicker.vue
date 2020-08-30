<template>
  <section style="root">
    <div class="select" :style="{ width }">
      <p class="placeholder">{{ value }}</p>
      <button class="btn-time" @click="clickHandler">
        <img src="../assets/timer.svg" width="3rem" class="btn-picture" />
      </button>
      <transition name="slide-fade">
        <div
          class="wrapper"
          :style="{ width: width + '50px', height: width + '100px' }"
          v-if="active"
        >
          <div
            class="clock-wrapper"
            :style="{ width, height: width }"
            :class="{ active }"
          >
            <div class="clock" :style="{ 'background-color': backgroundColor }">
              <div
                class="clock-theme"
                :style="{ width, height: width, backgroundSize: width }"
              >
                <div
                  class="container"
                  :style="{ width: width / 10, heigh: width / 10 }"
                  v-for="idx in 12"
                  :key="idx"
                >
                  <div
                    class="block"
                    :style="{
                      transform: `rotate(${idx * 30}deg)`,
                      width: width / 2,
                      height: width / 6
                    }"
                  >
                    <button
                      class="square"
                      :style="{
                        transform: `rotate(${270 - idx * 30}deg)`,
                        width: width / 10,
                        heigh: width / 10
                      }"
                      @click="selectHour(idx)"
                    >
                      {{ layoutFromOne ? idx : idx + 12 }}
                    </button>
                  </div>
                </div>
              </div>
            </div>
            <button class="btn-next" @click="nextHourLayout">
              <img src="../assets/next.svg" width="2rem" class="btn-picture" />
            </button>
          </div>
        </div>
      </transition>
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
  z-index: 10000;
}
.block {
  width: 150px;

  height: 50px;
  display: flex;

  align-items: center;
  transform-origin: 89%;
  position: absolute;
  bottom: -1.5rem;
}
.container {
  align-items: center;
  transform: rotate(90deg);
  transform-origin: 100%;
  top: 1rem;
  position: absolute;
}
.root {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.square {
  border: none;
  background: none;
  z-index: 30;
  width: 30px;
  height: 30px;
  color: #000;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  font-size: 1rem;
  font-weight: 800;
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
  position: absolute;
  left: 0;
  right: 0;
  opacity: 0;
  top: -400px;
  margin: 0 auto;
  border: 10px solid #ccc;
  width: 300px;
  height: 300px;
  border-radius: 100%;
  z-index: 100;
  display: none;
  text-align: center;
  z-index: -1;
  box-shadow: 5px 10px 10px rgb(107, 107, 107);
}
.wrapper {
  left: 0;
  right: 0;
  margin: 0 auto;
  height: 410px;
  width: 350px;
  position: absolute;
  top: 30px;
  display: flex;
  justify-content: center;
  overflow: hidden;
  z-index: -1;
}
.active {
  display: block;
  opacity: 1;
  top: 20px;
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
.slide-fade-enter {
  transform: translateY(-200px);
  opacity: 0;
}
.slide-fade-enter-active {
  transition: all 0.3s;
}
.slide-fade-enter-to {
  transform: translateY(10px);
  opacity: 1;
}
.slide-fade-leave-active {
  transition: all 0.3s;
}
.slide-fade-leave-to,
.slide-fade-leave {
  transform: translateY(-200px);
  opacity: 0;
}
</style>
