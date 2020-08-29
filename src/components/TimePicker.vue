<template>
  <section>
    <div class="select" :style="{ 'width': this.width }">
      <p class="placeholder">{{ this.value }}</p>
      <button class="btn-time" @click="clickHandler">
        <img src="../assets/timer.svg" width="3rem" class="btn-picture" />
      </button>
    </div>
    <div class="clock-wrapper" :class="{ active }">
      <div class="clock" :style="{ 'background-color': this.backgroundColor }">
        <div class="clock-theme"></div>
      </div>
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
    active: false
  }),
  methods: {
    clickHandler() {
      console.log(this.backgroundColor);
      this.active = !this.active;
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

.select::before {
  /*content: "select time  |HH| : |MM|";*/
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
  margin-top: 5rem;
  border: 10px solid #ccc;
  width: 300px;
  height: 300px;
  border-radius: 100%;
  z-index: 100;
  display: none;
}
.active {
  display: block;
}
.clock {
  position: relative;
  z-index: -1;
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
}
</style>
