<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">&divide;</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "0";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : this.current * -1;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      if (this.current === "0") {
        this.current = "";
      }

      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.includes(".")) {
        return;
      }
      if (this.current.includes("0")) {
        this.current = "0.";
      } else if (this.current.indexOf("." === -1)) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => +a / +b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => +a * +b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => +a - +b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => +a + +b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(this.previous, this.current)}`;
      this.previous = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  max-width: 500px;
  margin: 0 auto;
  font-size: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  box-shadow: rgba(0, 0, 0, 0.07) 0px 1px 1px, rgba(0, 0, 0, 0.07) 0px 2px 2px,
    rgba(0, 0, 0, 0.07) 0px 4px 4px, rgba(0, 0, 0, 0.07) 0px 8px 8px,
    rgba(0, 0, 0, 0.07) 0px 16px 16px;
}
.display {
  grid-column: 1/5;
  background-color: #40739e;
  color: #fff;
  text-align: right;
  padding-right: 10px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.btn {
  padding: 15px 0;
  background-color: #eee;
  border: 1px solid #999;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.btn:active {
  transform: scale(0.95);
}
.zero {
  grid-column: 1/3;
}
.operator {
  background-color: #f0932b;
  color: #fff;
}
</style>
