<template>
  <div id="loader" class="load"
  :class="{'dialog-hide' : !isShowLoader}">
    <div class="loadData"></div>
  </div>
</template>

<script>
export default {
  name: "loader",
  props: {
      isShowLoader: {
          type: Boolean,
          default: false

      }
  }
};
</script>

<style scoped>
#loader {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  align-items: center;
}
.loadData {
  position: absolute;
  top:50%;
  left: 50%;
  align-items: center;
  flex-shrink: 0;
  width: 50px;
  height: 50px;
  background-image: url("../../src/assets/loading.svg");
  background-size: contain;
  background-position: left;
  background-repeat: no-repeat;
}
</style>