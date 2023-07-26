<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">Calculator</h1>

    <!-- Calculator Display -->
    <div class="calculator-display text-right mb-3">
      <h1>{{ current || "0" }}</h1>
    </div>

    <div class="calculator">
      <tbody>
        <!-- Calculator Buttons Rows -->
        <!-- Row 1 -->
        <tr>
          <td @click="onOperatorClick('C')" class="btn-operator">C</td>
          <td @click="onOperatorClick('-/+')" class="btn-operator"><i class="fa-solid fa-plus-minus"></i></td>
          <td @click="onOperatorClick('%')" class="btn-operator"><i class="fa-solid fa-percent"></i></td>
          <td @click="onOperatorClick('/')" class="btn-operator"><i class="fa-solid fa-divide"></i></td>
        </tr>

        <!-- Row 2 -->
        <tr>
          <NumberButtonRow v-for="number in ['7', '8', '9']" :key="number" :number="number" @number-clicked="append" />
          <td @click="onOperatorClick('*')" class="btn-operator"><i class="fa-solid fa-xmark"></i></td>
        </tr>

        <!-- Row 3 -->
        <tr>
          <NumberButtonRow v-for="number in ['4', '5', '6']" :key="number" :number="number" @number-clicked="append" />
          <td @click="onOperatorClick('-')" class="btn-operator"><i class="fa-solid fa-minus"></i></td>
        </tr>

        <!-- Row 4 -->
        <tr>
          <NumberButtonRow v-for="number in ['1', '2', '3']" :key="number" :number="number" @number-clicked="append" />
          <td @click="onOperatorClick('+')" class="btn-operator"><i class="fa-solid fa-plus"></i></td>
        </tr>

        <!-- Row 5 -->
        <tr>
          <td @click="decimalPoint" class="btn-number">.</td>
          <NumberButtonRow number="0" @number-clicked="append" />
          <td @click="equal" class="btn-equal" :colspan="2"><i class="fa-solid fa-equals"></i></td>
        </tr>
      </tbody>
    </div>
  </div>
</template>

<script>
import './calculator-app.css';
import NumberButtonRow from './NumberButtonRow.vue';

export default {
  name: "Calculator", // eslint-disable-line
  components: { NumberButtonRow },


  data() {
    return {
      current: "0",
    };
  },
  methods: {
  
    // Append a number to the current number on button click
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },

    onOperatorClick(operator) {
      switch (operator) {
        case '+': {
          this.operator = (a, b) => a + b;
          this.setPrevious();
          break;
        }
        case '-':
          {
            this.operator = (a, b) => a - b;
            this.setPrevious();
            break;
          }
        case '*': {
          this.operator = (a, b) => a * b;
          this.setPrevious();
          break;
        }
        case '/': {
          this.operator = (a, b) => a / b;
          this.setPrevious();
          break;
        }
        case '%': {
          this.current = `${parseFloat(this.current) / 100}`;
          break;
        }
        case '-/+': {
          this.current =
            this.current.charAt(0) === "-" ? this.current.slice(1) : `-${this.current}`;
          break;
        }

        case 'C': {
          this.current = "";
          break;
        }
        case '.': {
          if (this.current.indexOf('.') === -1) {
            this.append('.');

          } 
          break;
        }
        default:
          this.operator = null;
      }
    },
    // Set the previous value and operator when an operator button is clicked
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    // Set the divide operator and prepare for the next number input

    // Calculate the final result when the equal button is clicked
    equal() {
      if (this.operator && this.previous) {
        this.current = this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        ).toString();
        this.previous = null;
        this.operatorClicked = false;
      }
    },

  }
};
</script>
