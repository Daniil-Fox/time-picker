<template>
  <section>
    <div class="select" @click="clickHandler">
      <p class="placeholder">HH MM</p>
      <button class="btn-time">Select</button>
    </div>
    <div class="clock-wrapper" :class="{active}">
      <div class="clock">
        <div class="clock-theme"></div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  data: () => ({
    active: false
    
  }),
  methods: {
    clickHandler() {
      this.active = !this.active;
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
  height: 30px;
}

.select::before {
  content: "select time  |HH| : |MM|";
  color: #868686;
  position: absolute;
  text-transform: uppercase;
  padding: 5px;
}
.btn-time {
  position: absolute;
  right: 0;
  height: inherit;
  border-radius: 50%;
  width: 50px;
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
  background: linear-gradient(45deg, rgb(255, 100, 100), rgb(12, 49, 255));
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
