<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">×</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="zero btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equalTo" class="btn operator">=</div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HelloWorld",
  data() {
    return {
      current: "",
      previous: null as unknown as string,
      operator: null as unknown as Function,
      operatorClick: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number: number | string) {
      if (this.operatorClick) {
        this.current = "";
        this.operatorClick = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current === "") {
        this.append(0);
      }
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClick = true;
    },
    divide() {
      this.operator = (a: number, b: number) => {
        return a / b;
      };
      this.setPrevious();
    },
    times() {
      this.operator = (a: number, b: number) => {
        return a * b;
      };
      this.setPrevious();
    },
    minus() {
      this.operator = (a: number, b: number) => {
        return a - b;
      };
      this.setPrevious();
    },
    add() {
      this.operator = (a: number, b: number) => {
        return a + b;
      };
      this.setPrevious();
    },
    equalTo() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = "";
    },
  },
});
</script>

<style scoped>
.calculator {
  border: 1px solid #5f5f5f;
  border-radius: 5px;
  margin: auto;
  width: 400px;
  text-align: center;
  font-size: 25px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  padding-top: 8px;
  border: 1px solid #5f5f5f;
  border-radius: 5px;
  grid-column: 1/5;
  background-color: #333;
  color: whitesmoke;
}

.zero {
  grid-column: 1/3;
}
.btn {
  margin: 2px;
  padding-top: 6px;
  background-color: rgb(74, 78, 92);
  border: none;
  color: rgb(160, 160, 160);
}
.btn:hover {
  margin: 2px;
  padding-top: 6px;
  background-color: rgb(231, 231, 231);
  border: none;
  color: rgb(128, 110, 110);
}
.operator {
  background-color: rgba(255, 166, 0, 0.721);
  color: aliceblue;
}
</style>
