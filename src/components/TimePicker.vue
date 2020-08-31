<template>
  <section style="root">
    <div class="select" :style="{ width }">
      <p class="placeholder">{{ selectedTime }}</p>
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
            <div class="clock" :style="{ backgroundColor }">
              <div
                class="clock-theme"
                :style="{ width, 'height': width, backgroundSize: width }"
              >
                <div
                  class="container"
                  :style="{ width: width / 10, heigh: width / 10 }"
                  v-for="(key, idx) in arrow"
                  :key="idx"
                >
                  <div
                    class="block"
                    :style="{
                      transform: `rotate(${key.idx * 30}deg)`,
                    }"
                  >
                    <select
                      v-if="key.show"
                      v-model="key.show"
                      class="clock-hand"
                      :style="{ backgroundColor: 'red' }"
                    />
                    <button
                      class="square"
                      :style="{
                        transform: `rotate(${270 - key.idx * 30}deg)`,
                        
                      }"
                      @click="selectHour(key.idx)"
                    >
                      {{ layoutFromOne ? key.idx : key.idx + 12 }}
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <button class="btn-next" @click="nextHourLayout">
              <img src="../assets/next.svg" class="btn-picture" />
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
    arrow: [
      {idx: 1, show: false},
      {idx: 2, show: false},
      {idx: 3, show: false},
      {idx: 4, show: false},
      {idx: 5, show: false},
      {idx: 6, show: false},
      {idx: 7, show: false},
      {idx: 8, show: false},
      {idx: 9, show: false},
      {idx: 10, show: false},
      {idx: 11, show: false},
      {idx: 12, show: false},
    ],

    active: false,
    
    hour: null, //здесь тип не определяется, не пропса же
    minute: null,
    time: "hh:mm:ss",
    layoutFromOne: true
  }),
  methods: {
    clickHandler() {
      console.log(this.backgroundColor);
      this.active = !this.active;
    },
    selectHour(idx) {
      this.hour = idx;
      this.time = this.formatTime(this.hour);
      this.arrow
        .map(arr => {
          arr.show = false
          if(arr.idx === idx || arr.idx - 12 === idx){
            arr.show = true
          }
        })
    },
    nextHourLayout() {
      this.layoutFromOne = !this.layoutFromOne;
    },
    formatTime(hour) {
      return `${hour}:00:00`; // строковый формат поменять на числовой
    }
  }, 
  computed: {
    selectedTime(){
      if(!this.layoutFromOne){
        return this.hour + 12 + ':00:00' // строковый формат поменять на числовой
      }
      return this.time
    }
  }
};
</script>



<style lang="scss" scoped>
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
  text-align: center;
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
  font-weight: 700;
}
.clock-hand {
  position: absolute;
  border: none;
  transform-origin: 0%;
  transform: rotate(1deg);
  height: 2px;
  width: 120px;
}
.blockActive {
  border: 1px solid #000;
}
.select::before {
  color: #868686;
  position: absolute;
  text-transform: uppercase;
  padding: 5px;
}
.btn-field {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.btn-picture {
  width: 1.8rem;
}
.btn-time {
  border: 0px;
  background: none;
  outline: none;
  position: absolute;
  right: 0;
  width: 2.5rem;
}

.btn-next {
  margin-top: 1.8rem;
  border-radius: 50%;
  border: 2px solid rgb(104, 104, 104);
  width: 3rem;
  height: 3rem;
  background: none;
}
.placeholder {
  display: block;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 1rem;
}
.clock-wrapper {
  position: absolute;
  left: 0;
  right: 0;
  opacity: 0;
  top: -400px;
  border: 10px solid #ccc;
  width: 300px;
  height: 300px;
  border-radius: 100%;
  z-index: 100;
  display: none;
  text-align: center;
  z-index: -1;
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
