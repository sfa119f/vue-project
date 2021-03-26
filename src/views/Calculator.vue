<template>
  <div class="container-fluid">
    <h1>Calculator</h1>
    <div class="calc__container">
      <div class="calc__input">
        <label for="input1">Input 1</label>
        <br>
        <input v-model="input1" type="number" name="input1" id="input1" @keypress="isNumber($event)">
      </div>
      <div class="calc__input">
        <label for="input2">Input 2</label>
        <br>
        <input v-model="input2" type="number" name="input2" id="input2" @keypress="isNumber($event)">
      </div>
      <div class="calc__input">
        <label for="operation">Operation</label>
        <br>
        <select v-model="operation" name="operation" id="operation">
          <option value="add">Additional</option>
          <option value="sub">Subtraction</option>
          <option value="mlt">Multiplication</option>
          <option value="div">Division</option>
        </select>
      </div>
      <div class="calc__btnresult">
        <button @click="getResult">Result</button>
      </div>
      <div id="calc-result" class="calc__result">
        {{ result }}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Calculator",
    data: () => {
      return{
        input1: "",
        input2: "",
        operation: "",
        result: "-"
      }
    },
    methods: {
      isNumber: function(evt) {
        var temp = (evt) ? evt : window.event;
        let charCode = (temp.which) ? temp.which : temp.keyCode;
        if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46 && charCode !== 45) {
          evt.preventDefault();
        } 
        else {
          return true;
        }
      },
      getResult: function() {
        if (this.input1 != "" && this.input2 != "" && this.operation != ""){
          switch (this.operation) {
            case "add":
              this.result = Number((parseFloat(this.input1) + parseFloat(this.input2)).toFixed(5));
              break;
            case "sub":
              this.result = Number((parseFloat(this.input1) - parseFloat(this.input2)).toFixed(5));
              break;
            case "mlt":
              this.result = Number((parseFloat(this.input1) * parseFloat(this.input2)).toFixed(5));
              break;
            case "div":
              this.result = Number((parseFloat(this.input1) / parseFloat(this.input2)).toFixed(5));
              break;
            default:
              this.result = "Undefine Operation"
          }
        }
        else {
          this.result = "Error Blank Input"
        }
      }
    }
  }
</script>

<style>
  @import '../assets/style/calculator.css';
</style>