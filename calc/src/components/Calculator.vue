<template>
  <div class="calculator">
    <h1>Calculator</h1>
    <input v-model.number="num1" type="number" placeholder="First number" />
    <br />
    <input v-model.number="num2" type="number" placeholder="Second number" />
    <p class="result">Result: {{ res }}</p>
    <div class="operations">
      <button class="btn btn-operation" @click="calculate('+')">+</button>
      <button class="btn btn-operation" @click="calculate('-')">-</button>
      <button class="btn btn-operation" @click="calculate('/')">/</button>
      <button class="btn btn-operation" @click="calculate('*')">x</button>
      <button class="btn btn-operation" @click="calculate('x^')">
        x<sup>y</sup>
      </button>
    </div>
    <label class="check">
      <input class="check__input" type="checkbox" v-model="keyboard" />
      <span class="check__box"></span>
      Show keyboard
    </label>
    <div class="keyboard" v-show="keyboard">
      <div class="numbers">
        <button
          class="btn btn-number"
          v-for="key in keys"
          :key="key"
          @click="setNumber(key)"
        >
          {{ key }}
        </button>
        <button class="btn btn-backspace" @click="backspaceNumber"></button>
      </div>
      <div class="operands">
        <label class="ratio">
          <input
            class="ratio__input"
            type="radio"
            name="operand"
            value="1"
            v-model="operand"
          />
          <span class="ratio__box"></span>
          Operand 1
        </label>
        <label class="ratio">
          <input
            class="ratio__input"
            type="radio"
            name="operand"
            value="2"
            v-model="operand"
          />
          <span class="ratio__box"></span>
          Operand 2
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    num1: 0,
    num2: 0,
    res: 0,
    keyboard: false,
    keys: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
    operand: '1',
  }),
  methods: {
    calculate(operator) {
      switch (operator) {
        case '+': {
          this.res = this.num1 + this.num2;
          break;
        }
        case '-': {
          this.res = this.num1 - this.num2;
          break;
        }
        case '/': {
          this.res =
            this.num2 === 0
              ? 'Error. You can not divide by zero'
              : this.num1 / this.num2;
          break;
        }
        case '*': {
          this.res = this.num1 * this.num2;
          break;
        }
        case 'x^': {
          this.res = Math.pow(this.num1, this.num2);
          break;
        }
      }
    },

    showKeyboard() {
      this.keyboard = !this.keyboard;
    },

    setNumber(number) {
      if (this.operand === '1')
        this.num1 =
          this.num1 === 0 ? number : parseInt(this.num1.toString() + number);
      else
        this.num2 =
          this.num2 === 0 ? number : parseInt(this.num2.toString() + number);
    },

    backspaceNumber() {
      if (this.operand === '1')
        this.num1 =
          this.num1 === 0
            ? this.num1
            : parseInt(this.num1.toString().slice(0, -1));
      else
        this.num2 =
          this.num2 === 0
            ? this.num2
            : parseInt(this.num2.toString().slice(0, -1));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
input {
  font-size: 20px;
  padding: 5px;
  text-align: center;
}

input:not(:last-child) {
  margin-top: 10px;
}

.result {
  font-size: 30px;
  margin: 20px 0;
}

.operations {
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn {
  font-size: 20px;
  padding: 10px 15px;
  color: white;
  background-color: orange;
  border: none;
  outline: none;
  border-radius: 10px;
  min-width: 50px;
  min-height: 50px;

  &-backspace {
    grid-column: 3/5;
    background-image: url("data:image/svg+xml,%3C%3Fxml version='1.0' encoding='iso-8859-1'%3F%3E%3Csvg version='1.1' id='Capa_1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' x='0px' y='0px' fill='%23ffffff' viewBox='0 0 512 512' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cpath d='M492,236H68.442l70.164-69.824c7.829-7.792,7.859-20.455,0.067-28.284c-7.792-7.83-20.456-7.859-28.285-0.068 l-104.504,104c-0.007,0.006-0.012,0.013-0.018,0.019c-7.809,7.792-7.834,20.496-0.002,28.314c0.007,0.006,0.012,0.013,0.018,0.019 l104.504,104c7.828,7.79,20.492,7.763,28.285-0.068c7.792-7.829,7.762-20.492-0.067-28.284L68.442,276H492 c11.046,0,20-8.954,20-20C512,244.954,503.046,236,492,236z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E%0A");
    background-repeat: no-repeat;
    background-size: 50%;
    background-position: center;
  }
}

.btn:active {
  opacity: 0.7;
}

.btn:not(:last-child) {
  margin-right: 5px;
}

.check {
  display: inline-block;
  margin: 30px 0;
  font-size: 20px;
  padding-left: 20px;
}

.check__input,
.ratio__input {
  position: absolute;
  appearance: none;
}

.check__box {
  position: absolute;
  width: 18px;
  height: 18px;
  box-shadow: 0 0 0 2px orange;
  margin-top: 3px;
  margin-left: -30px;
  transition: 0.5s all;
}

.check__input:checked + .check__box {
  background-color: orange;
  background-image: url("data:image/svg+xml,%3C%3Fxml version='1.0' encoding='iso-8859-1'%3F%3E%3Csvg version='1.1' id='Layer_1' xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink' x='0px' y='0px' viewBox='0 0 512 512' xml:space='preserve'%3E%3Cg%3E%3Cg%3E%3Cpath d='M504.502,75.496c-9.997-9.998-26.205-9.998-36.204,0L161.594,382.203L43.702,264.311c-9.997-9.998-26.205-9.997-36.204,0 c-9.998,9.997-9.998,26.205,0,36.203l135.994,135.992c9.994,9.997,26.214,9.99,36.204,0L504.502,111.7 C514.5,101.703,514.499,85.494,504.502,75.496z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E%0A");
}

.numbers {
  display: grid;
  grid-template-columns: repeat(4, 50px);
  justify-content: center;
  gap: 5px;
}

.operands {
  margin-top: 20px;
}

.ratio:not(:last-child) {
  margin-right: 40px;
}

.ratio__box {
  position: absolute;
  width: 14px;
  height: 14px;
  box-shadow: 0 0 0 2px orange;
  border-radius: 50%;
  margin-left: -25px;
  margin-top: 3px;
}

.ratio__input:checked + .ratio__box {
  background: radial-gradient(orange 20%, transparent 30%);
}
</style>
