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
              v-bind:class="{
                'ageSpan-deact': true,
                'ageSpan-act': false,
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
          <!-- v-if="objects[index - 1].age == 15" -->
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
      lifeSpanObj: [
        { name: "Gautama Buddha", yob: 565, yod: 651 },
        { name: "Bodhidharma", yob: 483, yod: 540 },
        { name: "Confucius", yob: 550, yod: 678 },
        { name: "Mahatma Gandhi", yob: 1869, yod: 1948 },
        { name: "Swami Vivekananda", yob: 1863, yod: 1902 },
        { name: "Thomas Alva Edison", yob: 1847, yod: 1931 },
        { name: "Albert Einstein", yob: 1879, yod: 1955 },
        { name: "Karl Marx", yob: 1818, yod: 1883 },
        { name: "Babur", yob: 1483, yod: 1531 },
        { name: "Isaac Newton", yob: 1643, yod: 1727 },
        { name: "Plato", yob: 426, yod: 546 },
        { name: "Chanakya", yob: 374, yod: 482 },
        { name: "Nicolaus Copernicus", yob: 1473, yod: 1543 },
        { name: "Harry Houdini", yob: 1874, yod: 1926 },
        { name: "Socrates", yob: 468, yod: 598 },
        { name: "William Shakespeare", yob: 1564, yod: 1616 },
        { name: "Adam Smith", yob: 1723, yod: 1790 },
        { name: "Subrahmanyan Chandrasekhar", yob: 1910, yod: 1995 },
        { name: "Archimedes", yob: 286, yod: 311 },
      ],
      rowArr: [],
      rowBcArr: [],
      colArr: [],
      arr:[[]],
      rowNumber: 0,
      rowNumberToClear:-1,
    };
  },
  methods: {
    changeName() {
      // console.log(this.lifeSpanObj);
      for (let index = 0; index < this.lifeSpanObj.length; index++) {
        const element = this.lifeSpanObj[index];
        setTimeout(() => {
          // this.rowArr.splice(0);
          // this.rowBcArr.splice(0);
          // this.colArr.splice(0);
          console.log("row number while clearing : " + this.rowNumber);
          this.arr[this.rowNumber] = [];
          console.log(this.arr);
          this.personName = element.name;
          // if (element.yob < 0) {
          //   this.rowNumber = 10 - Math.floor((-1 * element.yob) / 100) + 1;
          //   this.rowBcArr.push(this.rowNumber);
          // } else {
            this.rowNumber = Math.floor(element.yob / 100) + 1;
            // this.rowArr.push(this.rowNumber);
            this.arr[this.rowNumber] = [];
            if(this.rowNumberToClear  >= 0){
              this.arr[this.rowNumberToClear] = [];
              this.rowNumberToClear = -1;
            }
            let changeCen = element.yob;
            for (let i = element.yob; i < element.yod; i =i + 10) {
              let x = (i - Math.floor(i / 100) * 100);              
              if (Math.floor(i / 100) != Math.floor(changeCen / 100)){
                this.rowNumberToClear = this.rowNumber;
                this.rowNumber++;
               changeCen = i;
              }
              let col = x - (x % 10);
              // this.colArr.push(col/10);
                        console.log("row number while pushing : " + this.rowNumber);

              this.arr[this.rowNumber].push(col/10);
              // console.log("here is i : " + i + "rownumber : " +  this.rowNumber + "and col : " + col/10 + "and lief between" + element.yob + "and " + element.yod);
            }
          // }
          // if (element.yod < 0) {
          //   this.rowBcArr.push(10 - Math.floor((-1 * this.element.yob) / 100) + 1);
          // } else {
          //   this.rowArr.push(Math.floor(element.yod / 100) + 1);
          // }
        }, index * 2000);
      }
    },
  },
  mounted() {
    console.log("calling on page load");
    for (let index = 0; index < 21; index++) {
      this.arr[index] = []; 
    }
    axios({
      method: "GET",
      url: "https://dev-util.edyst.com/challenge/person/-1100?end_yob=2000",
    }).then(
      (result) => {
        console.log("success hit");
        // this.lifeSpanObj = result.data;
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