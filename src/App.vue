<template>
  <div id="app">
    <div class="calculator">
      <div class="inputFile">
        <input type="text" placeholder="0" v-model="temp" />
      </div>
      <div>
        <button v-on:click="porciento()">%</button>
        <button v-on:click="reiniciar()">CE</button>
        <button v-on:click="borrar()">C</button>
        <button v-on:click="div()">/</button>
      </div>
      <div>
        <button v-on:click="append('7')">7</button>
        <button v-on:click="append('8')">8</button>
        <button v-on:click="append('9')">9</button>
        <button v-on:click="mult()">X</button>
      </div>
      <div>
        <button v-on:click="append('4')">4</button>
        <button v-on:click="append('5')">5</button>
        <button v-on:click="append('6')">6</button>
        <button v-on:click="rest()">-</button>
      </div>
      <div>
        <button v-on:click="append('1')">1</button>
        <button v-on:click="append('2')">2</button>
        <button v-on:click="append('3')">3</button>
        <button v-on:click="sum()">+</button>
      </div>
      <div>
        <button v-on:click="append('0')">0</button>
        <button v-on:click="append('00')">00</button>
        <button>.</button>
        <button v-on:click="makeOperation()">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      num1: "",
      num2: "",
      operatorClick: false,
      resultado: null,
      operation: false,
      opSum: false,
      opRest: false,
      opMult: false,
      opDiv: false,
      opPorciento: false,
      temp: "",
    };
  },
  methods: {
    sum() {
      if (this.operation == true) {
        this.num1 = this.resultado;
        this.num2 = "";
        this.opSum = true;
        this.opDiv = false;
        this.opMult = false;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
      if (this.num1 !== "") {
        this.operation = true;
        this.opSum = true;
        this.opDiv = false;
        this.opMult = false;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
    },
    rest() {
      if (this.operation == true) {
        this.num1 = this.resultado;
        this.num2 = "";
        this.opSum = false;
        this.opDiv = false;
        this.opMult = false;
        this.opRest = true;
        this.opPorciento = false;
        return;
      }
      if (this.num1 !== "") {
        this.operation = true;
        this.opSum = false;
        this.opDiv = false;
        this.opMult = false;
        this.opRest = true;
        this.opPorciento = false;
        return;
      }
    },
    div() {
      if (this.operation == true) {
        this.num1 = this.resultado;
        this.num2 = "";
        this.opSum = false;
        this.opDiv = true;
        this.opMult = false;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
      if (this.num1 !== "") {
        this.operation = true;
        this.opSum = false;
        this.opDiv = true;
        this.opMult = false;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
    },
    mult() {
      if (this.operation == true) {
        this.num1 = this.resultado;
        this.num2 = "";
        this.opSum = false;
        this.opDiv = false;
        this.opMult = true;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
      if (this.num1 !== "") {
        this.operation = true;
        this.opSum = false;
        this.opDiv = false;
        this.opMult = true;
        this.opRest = false;
        this.opPorciento = false;
        return;
      }
    },
    borrar() {
      if (this.num2 == "") {
        this.num1 = "";
        this.temp = this.num1;
      } else if (this.num1 !== "") {
        this.num2 = "";
        this.temp = this.num2;
      }
    },
    reiniciar() {
      this.resultado = null;
      this.num1 = "";
      this.num2 = "";
      this.temp = "";
      this.operation = false;
    },
    porciento() {
      this.opPorciento = true;
      if (this.opPorciento == true) {
        this.resultado = parseFloat(parseInt(this.resultado) / 100);
        return (this.temp = this.resultado);
      }
    },
    makeOperation() {
      console.log(this.num1, this.num2);
      if (this.opSum == true) {
        this.resultado = parseFloat(parseInt(this.num1) + parseInt(this.num2));
        return (this.temp = this.resultado);
      } else if (this.opRest == true) {
        this.resultado = parseFloat(parseInt(this.num1) - parseInt(this.num2));
        return (this.temp = this.resultado);
      } else if (this.opDiv == true) {
        this.resultado = parseFloat(parseInt(this.num1) / parseInt(this.num2));
        return (this.temp = this.resultado);
      } else if (this.opMult == true) {
        this.resultado = parseFloat(parseInt(this.num1) * parseInt(this.num2));
        return (this.temp = this.resultado);
      }
    },
    append(num) {
      if (this.operation == false) {
        if (this.num1 !== "") {
          this.num1 = `${this.num1}${num}`;
        } else {
          this.num1 = `${this.num1}${num}`;
        }
        this.temp = this.num1;
      } else if (this.operation == true) {
        if (this.num2 !== "") {
          this.num2 = `${this.num2}${num}`;
        } else {
          this.num2 = `${this.num2}${num}`;
        }
        this.temp = this.num2;
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.calculator {
  background-color: rgb(211, 211, 211);
  width: 250px;
  height: 340px;
  margin: auto;
  justify-content: center;
  text-align: center;
  border-radius: 10px;
}

button {
  height: 50px;
  width: 50px;
  border-radius: 10px;
  margin: 1px;
}

input {
  text-align: right;
  width: 210px;
  margin: 10px;
  height: 42px;
  border-radius: 10px;
  font-size: medium;
}
</style>