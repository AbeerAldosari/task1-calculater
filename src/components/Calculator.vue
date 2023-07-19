<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">Calculator</h1>

    <!-- Calculator Display -->
    <div class="calculator-display text-right mb-3">
      <h1>{{ current || "0" }}</h1>
    </div>

    <div class="calculator">
      <table class="table table-bordered">
        <tbody>
          <!-- Calculator Buttons Rows -->
          <tr>
            <td @click="clear" class="btn-operator">C</td>
            <td @click="sign" class="btn-operator"><i class="fa-solid fa-plus-minus"></i></td>
            <td @click="percent" class="btn-operator"><i class="fa-solid fa-percent"></i></td>
            <td @click="divide" class="btn-operator"><i class="fa-solid fa-divide"></i></td>
          </tr>
          <tr>
            <td @click="append('7')" class="btn-number"><i class="fa-solid fa-7"></i></td>
            <td @click="append('8')" class="btn-number"><i class="fa-solid fa-8"></i></td>
            <td @click="append('9')" class="btn-number"><i class="fa-solid fa-9"></i></td>
            <td @click="times" class="btn-operator"><i class="fa-solid fa-xmark"></i></td>
          </tr>
          <tr>
            <td @click="append('4')" class="btn-number"><i class="fa-solid fa-4"></i></td>
            <td @click="append('5')" class="btn-number"><i class="fa-solid fa-5"></i></td>
            <td @click="append('6')" class="btn-number"><i class="fa-solid fa-6"></i></td>
            <td @click="minus" class="btn-operator"><i class="fa-solid fa-minus"></i></td>
          </tr>
          <tr>
            <td @click="append('1')" class="btn-number"><i class="fa-solid fa-1"></i></td>
            <td @click="append('2')" class="btn-number"><i class="fa-solid fa-2"></i></td>
            <td @click="append('3')" class="btn-number"><i class="fa-solid fa-3"></i></td>
            <td @click="add" class="btn-operator"><i class="fa-solid fa-plus"></i></td>
          </tr>
          <tr>
            <td @click="dot" class="btn-number">.</td>
            <td @click="append('0')" class="btn-number"><i class="fa-solid fa-0"></i></td>
            <td @click="equal" class="btn-equal" :colspan="2"><i class="fa-solid fa-equals"></i></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator", // eslint-disable-line

  data() {
    return {
      current: "1",
    };
  },
  methods: {
    // Clear the calculator display
    clear() {
      this.current = "";
    },
    // Change the sign of the current number (positive/negative)
    sign() {
      this.current =
        this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`;
    },
    // Calculate percentage of the current number
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    // Append a number to the current number on button click
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    // Append a decimal point to the current number
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    // Set the previous value and operator when an operator button is clicked
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    // Set the divide operator and prepare for the next number input
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    // Set the multiplication operator and prepare for the next number input
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    // Set the subtraction operator and prepare for the next number input
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    // Set the addition operator and prepare for the next number input
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    // Calculate the final result when the equal button is clicked
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }  
};
</script>


<style scoped>
.calculator-display {
  max-width: 300px; 
  margin: 0 auto;
  background-color: #f8f9fa;
  border-radius: 5px;
  padding: 10px;
  box-shadow: 0 6px 10px rgba(0, 0, 0, 0.1);
  font-size: 28px;
  color: #333;
}

.calculator {
  max-width: 300px; 
  margin: 0 auto;
}

.table {
  width: 100%;
}

.table td {
  cursor: pointer;
  text-align: center;
  font-size: 24px;
  padding: 10px;
  transition: background-color 0.2s ease;
}

.table td:hover {
  background-color: #f0f0f0;
}

.btn-number {
  background-color: #343a40;
  color: #ffffff;
}

.btn-number:hover {
  background-color: #23272b;
}

.btn-operator {
  background-color: #6c757d;
  color: #ffffff;
}

.btn-operator:hover {
  background-color: #545b62;
}

.btn-equal {
  background-color: #ffc107;
  color: #000000;
}

.btn-equal:hover {
  background-color: #ffa000;
}
</style>