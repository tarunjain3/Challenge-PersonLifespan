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
    <div class="row">
      <div class="col-sm-12">
        <h1>
          {{ personName }}
        </h1>
      </div>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      classChange: true,
      personName: "Initialize",
      lifeSpanObj: [],
    };
  },
  methods: {
    changetheClass() {
      this.classChange = !this.classChange;
    },
    changeName() {
      this.personName = "def  abc";
      this.lifeSpanObj.forEach((element, i) => {
        setTimeout(function () {
          this.personName = element.name;
          console.log(this.personName);
          console.log(i);
        }, i * 300);
      });
    },
  },
  mounted() {
    console.log("calling on page load");
    axios({
      method: "GET",
      url: "https://dev-util.edyst.com/challenge/person/-1100?end_yob=2000",
    }).then(
      (result) => {
        console.log("success hit");
        this.lifeSpanObj = result.data;
        return this.changeName();
      },
      (error) => {
        console.error(error);
      }
    );
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
  margin: 0.05% 0.025% 0% 0.025%;
  height: 8px;
  width: 8px;
  background-color: grey;
}
</style>