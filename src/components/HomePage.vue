<template>
  <div class="container" style="float: right">
    <div class="row">
      <div class="col-lg-1">
        <p>1</p>
      </div>
      <div v-for="index in 3" :key="index.id">
        <!-- v-if="objects[index - 1].age == 15" -->
        <div class="col-lg-1">
          <div
            :class="{
              'ageSpan-deact': !classChange,
              'ageSpan-act': classChange,
            }"
          ></div>
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
      classChange : true ,
      objects: [
        { name: "abc", age: 10 },
        { name: "def", age: 15 },
        { name: "xyz", age: 15 },
      ],
    };
  },
   methods: {
changetheClass(){
  this.classChange = !this.classChange;
}
      
    }
};
</script>
<style scoped>
.ageSpan-act {
  height: 16px;
  width: 16px;
  background-color: yellow;
}
.ageSpan-deact {
  margin: 8px 4px 0px 4px;
  height: 8px;
  width: 8px;
  background-color: grey;
}
</style>