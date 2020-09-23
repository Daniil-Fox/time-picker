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
          <div class="clock-wrapper" :style="{ width, height: width }" :class="{ active }">
            
          <transition name="turnover">
            <div class="clock" v-if="!next" :style="{ backgroundColor }">
              <div class="clock-theme" :style="{ width, height: width, backgroundSize: width }">
                <!-- here new clock for minutes-->
                <div
                  class="container"
                  :style="{ width: width / 10, heigh: width / 10 }"
                  v-for="(key, idx) in arrow"
                  :key="idx"
                >
                  <div
                    class="block"
                    :style="{
                      transform: `rotate(${key.idx * 30}deg)`
                    }"
                  >
                    <select
                      v-if="key.show"
                      v-model="key.show"
                      class="clock-hand"
                      :style="{ backgroundColor: 'red'}"
                    />
                    <button
                      class="square sq1"
                      :style="{
                        transform: `rotate(${270 - key.idx * 30}deg)`
                      }"
                      @click="selectHour(key.idx)"
                    >{{ key.idx  }}</button>

                    <button
                      class="square sq2"
                      :style="{
                        transform: `rotate(${270 - key.idx * 30}deg)`,
                      }"
                      @click="selectHour(key.idx + 12)"
                    >{{ key.idx + 12 }}</button>
                    
                  </div>
                </div>
              </div>
            </div>
          </transition>
          <!-- /////////////////////// -->
          <transition name="turnover">
              <div 
                  class="clock" 
                  v-if="next" 
                  :style="{ backgroundColor }">
                <div 
                  class="clock-theme" 
                  :style="{ width, height: width, backgroundSize: width }">
                  <!-- here new clock for minutes-->
                  <div
                    class="container"
                    :style="{ width: width / 10, heigh: width / 10 }"
                    v-for="(key, idx) in minutes"
                    :key="idx"
                  >
                    <div
                      class="block"
                      :style="{
                        transform: `rotate(${key.idx * 6}deg)`,
                          
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
                          transform: `rotate(${270 - key.idx * 6}deg)`,
                          fontSize: '.7rem',
                          width: '10px',
                          heigh: '10px',
                          margin: '-5px',
                         

                        }"
                        :class="{btnActive: selectHour}"
                        @click="selectMinute(key.idx)"
                      >{{ key.idx }}</button>
                      
                    </div>
                  </div>
                </div>
              </div>
            </transition>
            <button class="btn-next" :class="{disabled: !disabled}" @click="next = false, disabled = false">
              Back
            </button>
            <!-- <button  class="btn-next" :class="{disabled}" @click="nextHourLayout">
              <img src="../assets/next.svg" class="btn-picture" />
            </button> -->
            <button class="btn-next" :class="{disabled}" @click="next= true, disabled = true">
              Next
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
    arrow: new Array(12)
      .fill(0)
      .map((buff, idx) => ({ idx: idx + 1, show: false })),
    minutes: new Array(60)
      .fill(0)
      .map((buff, idx) => ({ idx: idx + 1, show: false })),
    active: false,
    next: false,
    disabled: false,
    hour: null, //здесь тип не определяется, не пропса же
    minute: null,
    time: "hh:mm",
    
  }),
  methods: {
    clickHandler() {
      console.log(this.backgroundColor);
      console.log(this.arrow);
      this.active = !this.active;
    },
    selectHour(idx) {
      this.hour = idx;
      this.time = this.formatTime();
      this.arrow.map(arr => {
        arr.show = false;
        if (arr.idx === idx || arr.idx + 12 === idx) {
          arr.show = true;
        }
      });
    },
    selectMinute(idx){
      this.minute = idx;
      this.time = this.formatTime();
      this.minutes.map(min => {
        min.show = false;
        if (min.idx === idx) {
          min.show = true;
        }
      });
    },
    formatTime() {
       if (this.hour && this.minute) {    
          return  this.minute < 10 ? `${this.hour}:0${this.minute}` :  `${this.hour}:${this.minute}`
       }
      if(this.hour){
        return `${this.hour}:00`
      }
       else {
         return '00:00'
       }
      
    },
    style() {}
  },
  computed: {
    selectedTime() {
      return this.time;
    },
    
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
  width: 300px;
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
  z-index: -1;
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
  z-index: 1;
}
.clock-hand {
  position: absolute;
  border: none;
  transform-origin: -30%;
  transform: rotate(1deg);
  height: 2px;
  width: 130px;
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
  cursor: pointer;
}
.placeholder {
  display: block;
  text-transform: uppercase;
  font-weight: 600;
  font-size: 1rem;
  position: absolute;

  left: 0;
  right: 0;
  margin: 0 auto;
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
  // overflow: hidden;
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
.turnover-enter-active {
  transition: all .2s ease;
}

.turnover-enter
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: rotate(-50deg);
}


.disabled {
  background: #ccc;
  pointer-events: none; 
  cursor: default;
}
.sq2 {
  border: 1px solid rgb(167, 167, 167);
  border-radius: 50%;
}
.btn-active {
  background: rgb(126, 126, 255);
}
</style>
