<template>
  <div class="container" style="float: right">
    <div v-for="rowIndex in 10" :key="rowIndex.id">
      <div class="row">
        <div class="col-sm-1">
          <p>{{ 1000 - (rowIndex - 1) * 100 }} BC</p>
        </div>
        <div v-for="index in 10" :key="index.id">
          <!-- v-if="objects[index - 1].age == 15" -->
          <div class="col-sm-1">
            <div
              :class="{
                'ageSpan-deact': !classChange,
                'ageSpan-act': classChange,
              }"
            ></div>
          </div>
        </div>
        <div class="col-sm-1 mar">{{ 1000 - rowIndex * 100 + 1 }} BC</div>
      </div>
    </div>
    <div v-for="rowIndex in 21" :key="rowIndex.id">
      <div class="row">
        <div class="col-sm-1">
          <p>{{ 1 + (rowIndex - 1) * 100 }} AC</p>
        </div>
        <div v-for="index in 10" :key="index.id">
          <!-- v-if="objects[index - 1].age == 15" -->
          <div class="col-sm-1">
            <div
              :class="{
                'ageSpan-deact': !classChange,
                'ageSpan-act': classChange,
              }"
            ></div>
          </div>
        </div>
        <div class="col-sm-1">{{ rowIndex * 100 }} AC</div>
      </div>
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
  margin: 0.05% 0.025% 0% 0.025%;
  height: 8px;
  width: 8px;
  background-color: grey;
}
</style>