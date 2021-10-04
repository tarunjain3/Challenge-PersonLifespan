<template>
  <div class="container" style="float: right">
    <div v-for="rowIndex in 10" :key="rowIndex.id">
      <div class="row">
        <div class="col-sm-1">
          <p>{{ 1000 - (rowIndex - 1) * 100 }} BC</p>
        </div>
        <div v-for="index in 10" :key="index.id">
          <div class="col-sm-1">
            <div
              v-bind:class="{
                'ageSpan-deact': !bcArr[rowIndex - 1].includes(index - 1),
                'ageSpan-act': bcArr[rowIndex - 1].includes(index - 1),
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
          <p>{{ 1 + (rowIndex - 1) * 100 }} AD</p>
        </div>
        <div v-for="index in 10" :key="index.id">
          <div class="col-sm-1">
            <div
              v-bind:class="{
                'ageSpan-deact': !arr[rowIndex - 1].includes(index - 1),
                'ageSpan-act': arr[rowIndex - 1].includes(index - 1),
              }"
            ></div>
          </div>
        </div>
        <div class="col-sm-1">{{ rowIndex * 100 }} AD</div>
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
      personName: "",
      lifeSpanObj: [],
      rowBcArr: [],
      arr: [[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],],
      rowNumber: 0,
      bcRowNumber: 0,
      rowNumberToClear: -1,
      bcRowNumberToClear: -1,
      bcArr: [[],[],[],[],[],[],[],[],[],[],[],[],[],[],[],],
    };
  },
  methods: {
    changeName() {
      // console.log(this.lifeSpanObj);
      for (let index = 0; index < this.lifeSpanObj.length; index++) {
        const element = this.lifeSpanObj[index];
        setTimeout(() => {
          this.rowBcArr.splice(0);
          this.arr[this.rowNumber] = [];
          this.arr[this.bcRowNumber] = [];
          if (this.bcRowNumberToClear >= 0) {
              this.bcArr[this.bcRowNumberToClear] = [];
              this.bcRowNumberToClear = -1;
            }
            if (this.rowNumberToClear >= 0) {
              this.arr[this.rowNumberToClear] = [];
              this.rowNumberToClear = -1;
            }
          console.log(this.arr);
          this.personName = element.name;
          if (element.yob < 0) {
            this.bcRowNumber = 10 - Math.floor((-1 * element.yob) / 100);
            this.arr[this.bcRowNumber] = [];
            if (this.bcRowNumberToClear >= 0) {
              this.bcArr[this.bcRowNumberToClear] = [];
              this.bcRowNumberToClear = -1;
            }
            if (this.rowNumberToClear >= 0) {
              this.arr[this.rowNumberToClear] = [];
              this.rowNumberToClear = -1;
            }
            let changeCen = element.yob;
            for (let i = element.yob; i < element.yod; i = i + 10) {
              let x = Math.abs(i - Math.ceil(i / 100) * 100);
              if (Math.ceil(i / 100) != Math.ceil(changeCen / 100)) {
                this.bcRowNumberToClear = this.bcRowNumber;
                this.bcRowNumber++;
                changeCen = i;
              }
              let col = x - (x % 10);
              col = col / 10
              this.bcArr[this.bcRowNumber].push(10 - col );
              // console.log(
              //   "here is i : " +
              //     i +
              //     "bcrownumber : " +
              //     this.bcRowNumber +
              //     "and col : " +
              //     col / 10 +
              //     "and lief between" +
              //     element.yob +
              //     "and " +
              //     element.yod
              // );
            }
          } else {
            this.rowNumber = Math.floor(element.yob / 100) + 1;
            this.bcArr[this.bcRowNumber] = [];
            if (this.bcRowNumberToClear >= 0) {
              this.bcArr[this.bcRowNumberToClear] = [];
              this.bcRowNumberToClear = -1;
            }
            if (this.rowNumberToClear >= 0) {
              this.arr[this.rowNumberToClear] = [];
              this.rowNumberToClear = -1;
            }
            let changeCen = element.yob;
            for (let i = element.yob; i < element.yod; i = i + 10) {
              let x = i - Math.floor(i / 100) * 100;
              if (Math.floor(i / 100) != Math.floor(changeCen / 100)) {
                this.rowNumberToClear = this.rowNumber;
                this.rowNumber++;
                changeCen = i;
              }
              let col = x - (x % 10);
              this.arr[this.rowNumber].push(col / 10);
              // console.log("here is i : " + i + "rownumber : " +  this.rowNumber + "and col : " + col/10 + "and lief between" + element.yob + "and " + element.yod);
            }
          }
        }, index * 2000);
      }
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
        this.lifeSpanObj = result.data.sort((a, b) => { return a.yob - b.yob;});
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
  margin: 0.05% 4px 0px 4px;
  height: 8px;
  width: 8px;
  background-color: grey;
}
</style>