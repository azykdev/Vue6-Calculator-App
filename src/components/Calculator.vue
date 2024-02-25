<template>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>

    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="back">⇐</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="addSymbol('/')">÷</div>

    <div class="btn" @click="addSymbol('7')">7</div>
    <div class="btn" @click="addSymbol('8')">8</div>
    <div class="btn" @click="addSymbol('9')">9</div>
    <div class="btn operator" @click="addSymbol('*')">x</div>

    <div class="btn" @click="addSymbol('4')">4</div>
    <div class="btn" @click="addSymbol('5')">5</div>
    <div class="btn" @click="addSymbol('6')">6</div>
    <div class="btn operator" @click="addSymbol('-')">-</div>

    <div class="btn" @click="addSymbol('1')">1</div>
    <div class="btn" @click="addSymbol('2')">2</div>
    <div class="btn" @click="addSymbol('3')">3</div>
    <div class="btn operator" @click="addSymbol('+')">+</div>

    <div class="btn zero" @click="addSymbol('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="result">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    back() {
      const arr = this.current.split('')
      arr.pop()
      this.current = arr.join('')
    },
    percent() {
      if (+this.current > 1) {
        this.current = `${parseFloat(this.current) / 100}`;
      }
    },
    addSymbol(number) {
      if (this.current == "0" && number == "0") {
        this.current = "";
      } else {
        if (this.current == "0") {
          this.current = "";
        }
        this.current = `${this.current}${number}`;
      }
    },
    dot() {
      if (!this.current.includes(".")) {
        this.current = `${this.current}.`;
      }
    },
    result() {
      this.current = eval(this.current);
    },
  },
  mounted() {
    document.onselectstart = new Function("return false");
  },
};
</script>

<style scoped>
.calculator {
  margin: 100px auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  text-align: center;
  font-family: monospace;
}

.display {
  grid-column: 1/5;
  background: #333;
  color: #eee;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: end;
  padding: 10px;
}

.zero {
  grid-column: 1/3;
}

.btn {
  border: 1px solid #999;
  background: #eee;
  cursor: pointer;
  transition: 0.2s opacity ease;
  padding: 10px 0;
}
.btn:hover {
  opacity: 0.5;
}

.operator {
  background: orange;
  color: #eee;
}
</style>
