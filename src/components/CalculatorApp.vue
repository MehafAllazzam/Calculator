<template>
  <!-- Calculator container -->
  <div class="shadow-lg p-3 rounded calculatorContainer">
    <!-- Display the current value -->
    <div class="w-full rounded m-1 p-3 lead font-weight-bold text-white bg-dark ">
      {{ current || 0 }}
    </div>
    <!-- First row of buttons -->
    <div class="row no-gutters">
      <!-- clear button -->
      <div class="col-6 ">
        <div @click="clear" class="hoverClass lead text-dark text-center m-1 py-3 bg-secondary rounded hover-class"> 
            C
        </div>
      </div>
      <!-- sign button -->
      <div class="col-3 ">
        <div @click="sign" class="hoverClass lead text-dark text-center m-1 py-3 bg-secondary rounded hover-class">
          -/+
        </div>
      </div>
      <!-- divide button -->
      <div class="col-3 ">
        <div @click="divide" class="hoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class "> 
          ÷
        </div>
      </div>
    </div>
    <!-- Second row of buttons -->
    <div class="row no-gutters">
      <!-- Number 7 button -->
      <div class="col-3 ">
        <div @click="append('7')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          7
        </div>
      </div>
      <!-- Number 8 button -->
      <div class="col-3 ">
        <div @click="append('8')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          8
        </div>
      </div>
      <!-- Number 9 button -->
      <div class="col-3 ">
        <div @click="append('9')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          9
        </div>
      </div>
      <!-- Multiply button -->
      <div class="col-3 ">
        <div @click="times" class="hoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          x
        </div>
      </div>
    </div>
    <!-- Third row of buttons -->
    <div class="row no-gutters">
      <!-- Number 4 button -->
      <div class="col-3 ">
        <div @click="append('4')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          4
        </div>
      </div>
      <!-- Number 5 button -->
      <div class="col-3 ">
        <div @click="append('5')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          5
        </div>
      </div>
      <!-- Number 6 button -->
      <div class="col-3 ">
        <div @click="append('6')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          6
        </div>
      </div>
      <!-- Subtract button -->
      <div class="col-3 ">
        <div @click="minus" class="hoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          -
        </div>
      </div>
    </div>
    <!-- Fourth row of buttons -->
    <div class="row no-gutters">
      <!-- Number 1 button -->
      <div class="col-3 ">
        <div @click="append('1')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          1
        </div>
      </div>
      <!-- Number 2 button -->
      <div class="col-3 ">
        <div @click="append('2')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          2
        </div>
      </div>
      <!-- Number 3 button -->
      <div class="col-3 ">
        <div @click="append('3')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          3
        </div>
      </div>
      <!-- add button -->
      <div class="col-3 ">
        <div @click="add" class="hoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          +
        </div>
      </div>
    </div>
    <!-- Fifth row of buttons -->
    <div class="row no-gutters">
      <!-- Number 0 button -->
      <div class="col-6 ">
        <div @click="append('0')" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          0
        </div>
      </div>
      <!-- dot button -->
      <div class="col-3 ">
        <div @click="dot" class="hoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          .
        </div>
      </div>
      <!-- eqal button -->
      <div class="col-3 ">
        <div @click="eqal" class="hoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class "> 
          =
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        previous: null, // Variable to store the previous value entered
        current: '', // Variable to store the current value entered
        operator: null, // Variable to store the operator function
        operatorClicked: false, // Flag to indicate if an operator has been clicked
      }
    },
    methods:{
      // Function to clear the current value
      clear(){
        this.current = '';
      },
      // Function to toggle the sign of the current value
      sign(){
        if(this.current && parseFloat(this.current) !== 0){
          if(this.current.charAt(0)=== '-'){
            this.current = this.current.slice(1) 
          }
          else{
            this.current = '-' + this.current;
          } 
        } 
      },
      // Function to append a number to the current value
      append(number){
        // If an operator has been clicked, reset the current value
        if(this.operatorClicked){
          this.current = '';
          this.operatorClicked = false;
        }
        // Prevent leading zeros
        if(number == 0 && this.current == ''){
          return
        }
        this.current = this.current + number;
      },
      // Function to add a decimal point to the current value
      dot(){
        // If there is no decimal point already
        if(this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      // Function to set the previous value to the current value and set the operator clicked flag
      Setprevious(){
        this.previous = this.current;
        this.operatorClicked = true;
      },
      // Function to set the operator to division
      divide(){
        this.operator = (a, b) => a / b;
        this.Setprevious();
      },
      // Function to set the operator to multiplication
      times(){
        this.operator = (a, b) => a * b;
        this.Setprevious();
      },
      // Function to set the operator to subtraction
      minus(){
        this.operator = (a, b) => a - b;
        this.Setprevious();
      },
      // Function to set the operator to addition
      add() {
        this.operator = (a, b) => a + b; 
        this.Setprevious();
      },
      // Function to evaluate the expression and display the result
      eqal() {
        if(this.previous === ''){
          this.previous = 0
        }
        this.current = this.operator(parseFloat(this.previous),parseFloat(this.current));
        this.previous = null;
      }
    }
  }
</script>

<style scoped>
  .hoverClass {
    transition: background-color 0.3s ease-in-out;
  }
  .hoverClass:hover {
    background: #eef3f8 !important;
    color:black !important;
    cursor: pointer;
  }
  .calculatorContainer{
    max-width: 400px; 
    margin: 50px auto; 
    background: rgb(44, 67, 88); 
    text-align: right;
  }
</style>