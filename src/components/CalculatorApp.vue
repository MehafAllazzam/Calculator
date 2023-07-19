<template>
  <!-- Calculator container -->
  <div class="shadow-lg p-3 rounded" style="max-width: 400px; margin: 50px auto; background: rgb(44, 67, 88); text-align: right;">
    <!-- Display the current value -->
    <div class="w-full rounded m-1 p-3 lead font-weight-bold text-white bg-dark ">
      {{ Current || 0 }}
    </div>
    <!-- First row of buttons -->
    <div class="row no-gutters">
      <!-- Clear button -->
      <div class="col-6 ">
        <div @click="Clear" class="HoverClass lead text-dark text-center m-1 py-3 bg-secondary rounded hover-class"> 
            C
        </div>
      </div>
      <!-- Sign button -->
      <div class="col-3 ">
        <div @click="Sign" class="HoverClass lead text-dark text-center m-1 py-3 bg-secondary rounded hover-class">
          -/+
        </div>
      </div>
      <!-- Divide button -->
      <div class="col-3 ">
        <div @click="Divide" class="HoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class "> 
          ÷
        </div>
      </div>
    </div>
    <!-- Second row of buttons -->
    <div class="row no-gutters">
      <!-- Number 7 button -->
      <div class="col-3 ">
        <div @click="Append('7')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          7
        </div>
      </div>
      <!-- Number 8 button -->
      <div class="col-3 ">
        <div @click="Append('8')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          8
        </div>
      </div>
      <!-- Number 9 button -->
      <div class="col-3 ">
        <div @click="Append('9')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          9
        </div>
      </div>
      <!-- Multiply button -->
      <div class="col-3 ">
        <div @click="Times" class="HoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          x
        </div>
      </div>
    </div>
    <!-- Third row of buttons -->
    <div class="row no-gutters">
      <!-- Number 4 button -->
      <div class="col-3 ">
        <div @click="Append('4')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          4
        </div>
      </div>
      <!-- Number 5 button -->
      <div class="col-3 ">
        <div @click="Append('5')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          5
        </div>
      </div>
      <!-- Number 6 button -->
      <div class="col-3 ">
        <div @click="Append('6')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          6
        </div>
      </div>
      <!-- Subtract button -->
      <div class="col-3 ">
        <div @click="Minus" class="HoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          -
        </div>
      </div>
    </div>
    <!-- Fourth row of buttons -->
    <div class="row no-gutters">
      <!-- Number 1 button -->
      <div class="col-3 ">
        <div @click="Append('1')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          1
        </div>
      </div>
      <!-- Number 2 button -->
      <div class="col-3 ">
        <div @click="Append('2')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          2
        </div>
      </div>
      <!-- Number 3 button -->
      <div class="col-3 ">
        <div @click="Append('3')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          3
        </div>
      </div>
      <!-- Add button -->
      <div class="col-3 ">
        <div @click="Add" class="HoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class">
          +
        </div>
      </div>
    </div>
    <!-- Fifth row of buttons -->
    <div class="row no-gutters">
      <!-- Number 0 button -->
      <div class="col-6 ">
        <div @click="Append('0')" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class "> 
          0
        </div>
      </div>
      <!-- Dot button -->
      <div class="col-3 ">
        <div @click="Dot" class="HoverClass lead text-white text-center m-1 py-3 bg-dark rounded hover-class">
          .
        </div>
      </div>
      <!-- Equal button -->
      <div class="col-3 ">
        <div @click="Equal" class="HoverClass lead text-white text-center m-1 py-3 bg-warning rounded hover-class "> 
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
        Previous: null, // Variable to store the previous value entered
        Current: '', // Variable to store the current value entered
        Operator: null, // Variable to store the operator function
        OperatorClicked: false, // Flag to indicate if an operator has been clicked
      }
    },
    methods:{
      // Function to clear the current value
      Clear(){
        this.Current = '';
      },
      // Function to toggle the sign of the current value
      Sign(){
        if(this.Current && parseFloat(this.Current) !== 0){
          if(this.Current.charAt(0)=== '-'){
            this.Current = this.Current.slice(1) 
          }
          else{
            this.Current = '-' + this.Current;
          } 
        } 
      },
      // Function to append a number to the current value
      Append(number){
        // If an operator has been clicked, reset the current value
        if(this.OperatorClicked){
          this.Current = '';
          this.OperatorClicked = false;
        }
        // Prevent leading zeros
        if(number == 0 && this.Current == ''){
          return
        }
        this.Current = this.Current + number;
      },
      // Function to add a decimal point to the current value
      Dot(){
        // If there is no decimal point already
        if(this.Current.indexOf('.') === -1) {
          this.Append('.');
        }
      },
      // Function to set the previous value to the current value and set the operator clicked flag
      SetPrevious(){
        this.Previous = this.Current;
        this.OperatorClicked = true;
      },
      // Function to set the operator to division
      Divide(){
        this.Operator = (a, b) => a / b;
        this.SetPrevious();
      },
      // Function to set the operator to multiplication
      Times(){
        this.Operator = (a, b) => a * b;
        this.SetPrevious();
      },
      // Function to set the operator to subtraction
      Minus(){
        this.Operator = (a, b) => a - b;
        this.SetPrevious();
      },
      // Function to set the operator to addition
      Add() {
        this.Operator = (a, b) => a + b; 
        this.SetPrevious();
      },
      // Function to evaluate the expression and display the result
      Equal() {
        if(this.Previous === ''){
          this.Previous = 0
        }
        this.Current = this.Operator(parseFloat(this.Previous),parseFloat(this.Current));
        this.Previous = null;
      }
    }
  }
</script>

<style scoped>
  .HoverClass {
    transition: background-color 0.3s ease-in-out;
  }
  .HoverClass:hover {
    background: #eef3f8 !important;
    color:black !important;
    cursor: pointer;
  }
</style>