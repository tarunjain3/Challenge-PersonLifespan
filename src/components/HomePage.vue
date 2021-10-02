<template>
  <div class="container" style="float: right">
    <div class="row">
      <div class="col-lg-1">
        <p>1</p>
      </div>
      <div v-for="index in 10" :key="index.id">
        <div class="col-lg-1">
          <div class="ageSpan-deact"></div>
        </div>
      </div>
      <div class="col-lg-1 mar">100</div>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      objects: [
        { name: "abc", age: 10 },
        { name: "def", age: 15 },
        { name: "xyz", age: 15 },
      ],
    };
  },
};
</script>
<style scoped>
.ageSpan-act {
  height: 16px;
  width: 16px;
  background-color: yellow;
}
.ageSpan-deact {
  height: 8px;
  width: 8px;
  background-color: grey;
}
</style>