<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <button class="btn" @click="clear">C</button>
    <button class="btn" @click="sign">+/-</button>
    <button class="btn" @click="percent">%</button>
    <button class="btn operator" @click="divide">&#247;</button>
    <button class="btn" @click="append(7)">7</button>
    <button class="btn" @click="append(8)">8</button>
    <button class="btn" @click="append(9)">9</button>
    <button class="btn operator" @click="times">x</button>
    <button class="btn" @click="append(4)">4</button>
    <button class="btn" @click="append(5)">5</button>
    <button class="btn" @click="append(6)">6</button>
    <button class="btn operator" @click="minus">-</button>
    <button class="btn" @click="append(1)">1</button>
    <button class="btn" @click="append(2)">2</button>
    <button class="btn" @click="append(3)">3</button>
    <button class="btn operator" @click="plus">+</button>
    <button class="zero btn" @click="append(0)">0</button>
    <button class="btn" @click="dot">.</button>
    <button class="btn operator" @click="calculate">=</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false,
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
    append(num) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    divide() {
      this.operator = (a, b) => b / a;
      // eslint-disable-next-line no-console
      console.log(this.operator)
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => b * a;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => b + a;
      this.setPrevious();
    },
    calculate() {
      // eslint-disable-next-line no-console
      console.log(this.current, this.previous)
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    setPrevious() {
      this.previous = this.current;
      // eslint-disable-next-line no-console
      console.log(this.previous);
      this.operatorClicked = true;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax (50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: #000;
  color: white;
  height: 60px;
  padding-top: 20px;
}
.zero {
  grid-column: 1 / 3;
  background-color: blueviolet;
}
.btn {
  background-color: #eee;
  border: 1px solid #333;
  height: 80px;
  font-size: 40px;
  cursor: pointer;
}

.btn:hover {
  background-color: #e5e5e5;
}

.operator {
  background-color: orange;
  color: #fff;
}
.operator:hover {
  background-color: orange;
}
</style>
