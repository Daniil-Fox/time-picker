<template>
  <section>
    <div class="select" @click="clickHandler">
      <p class="placeholder"></p>
      <button class="btn-time">
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
  border: 1px solid black;
  width: 300px;
  height: 2rem;
}

.select::before {
  content: "select time  |HH| : |MM|";
  color: #868686;
  position: absolute;
  text-transform: uppercase;
  padding: 5px;
}
.btn-picture {
  width: 1.8rem;
  height: inherit;
  margin: 0.1rem 0.2rem;
}
.btn-time {
  border: 0px;
  background: none;
  outline: none;
  position: absolute;
  right: 0;
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
