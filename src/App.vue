<template>
  <div class="wrapper">
    <TimePicker :backgroundColor="'#E5E5E5'"/>
  </div>
</template>
<script>
import TimePicker from "./components/TimePicker";
export default {
  components: {
    TimePicker
  }
};
</script>
<style lang="scss" scoped>
.wrapper {
  max-width: 100%;
  display: flex;
  justify-content: center;
  padding-top: 5rem;
}
</style>
