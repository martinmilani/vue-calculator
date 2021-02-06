<template>
  <div class="flex items-center justify-center h-screen bg-gray-200">
    <div class="w-80 bg-white rounded-xl overflow-hidden shadow-2xl">
      <Display :equation="equation" :display="display" />
      <Board
        :handleNumbers="handleNumbers"
        :handleAllClear="handleAllClear"
        :handleDelete="handleDelete"
        :handleOperators="handleOperators"
        :handleCalculate="handleCalculate"
        :handleDecimal="handleDecimal"
      />
    </div>
  </div>
</template>

<script>
import Display from "./components/Display";
import Board from "./components/Board";
import { ref } from "vue";
import { evaluate } from "mathjs";

export default {
  components: { Display, Board },
  setup() {
    const equation = ref("");
    const display = ref("0");

    function isZero(str) {
      return str === "0";
    }

    function isEmpty(str) {
      return str == "";
    }

    function divZero(str) {
      return str.includes("/0");
    }

    function haveOperators(str) {
      return str.match(/[+\-*/]/);
    }

    function matchLastOperator(str) {
      return str.match(/[*\-/+]$/);
    }

    function matchLastNumber(str) {
      return str.match(/[0-9.]$/);
    }

    function lastChar(str) {
      return str.substring(0, str.length - 1);
    }

    function includesEqual(str) {
      return str.includes("=");
    }

    function includesPeriod(str) {
      return str.includes(".");
    }

    function handleAllClear() {
      changeDisplay("0", "");
    }

    function maxNumbers(str) {
      return str.length <= 9;
    }

    function changeDisplay(displayVal, equationVal) {
      display.value = displayVal;
      equation.value = equationVal;
    }

    function substractLast(str) {
      return str.substring(0, str.length - 1);
    }

    function handleDelete() {
      if (!includesEqual(equation.value)) {
        if (display.value.length === 1) {
          changeDisplay("0", substractLast(equation.value));
        } else {
          changeDisplay(
            substractLast(display.value),
            substractLast(equation.value)
          );
        }
      }
    }

    function handleOperators(e) {
      if (includesEqual(equation.value)) {
        //toma el resultado y lo incluye en la operacion
        changeDisplay(
          e.currentTarget.value,
          display.value + e.currentTarget.value
        );
      } else if (
        !isEmpty(equation.value) &&
        !matchLastOperator(equation.value)
      ) {
        // la acuacion no tiene operadores
        changeDisplay(
          e.currentTarget.value,
          equation.value + e.currentTarget.value
        );
      } else {
        if (matchLastOperator(equation.value)) {
          // cambia el operador
          changeDisplay(
            e.currentTarget.value,
            substractLast(equation.value) + e.currentTarget.value
          );
        }
      }
    }

    function handleNumbers(e) {
      if (maxNumbers(display.value)) {
        //cantidad maxima de digitos 10
        if (matchLastNumber(equation.value) && !includesEqual(equation.value)) {
          if (!matchLastOperator(equation.value)) {
            changeDisplay(
              equation.value + e.currentTarget.value,
              equation.value + e.currentTarget.value
            );
          } else {
            changeDisplay(
              display.value + e.currentTarget.value,
              equation.value + e.currentTarget.value
            );
          }
        } else {
          if (matchLastOperator(equation.value)) {
            changeDisplay(
              e.currentTarget.value,
              equation.value + e.currentTarget.value
            );
          } else {
            if (
              (isZero(display.value) && !isZero(e.currentTarget.value)) ||
              includesEqual(equation.value)
            ) {
              changeDisplay(e.currentTarget.value, e.currentTarget.value);
            }
          }
        }
      } else {
        window.alert("Max - 10 digits!");
      }
    }

    function handleCalculate() {
      if (
        !includesEqual(equation.value) &&
        !isEmpty(equation.value) &&
        haveOperators(equation.value) &&
        !matchLastOperator(equation.value)
      )
        if (divZero(equation.value)) {
          changeDisplay("ERROR", "can't divide by 0");
        } else {
          let result = Math.round(evaluate(equation.value) * 1000) / 1000;
          if (result >= 999999) {
            result = result.toExponential(3);
          }
          let resultStr = result.toString();
          changeDisplay(resultStr, equation.value + "=" + resultStr);
        }
    }

    function handleDecimal(e) {
      if (isEmpty(equation.value) || includesEqual(equation.value)) {
        changeDisplay("0.", "0.");
      } else if (haveOperators(equation.value)) {
        changeDisplay("0.", equation.value + "0.");
      } else if (!includesPeriod(display.value)) {
        changeDisplay(
          display.value + e.currentTarget.value,
          equation.value + e.currentTarget.value
        );
      }
    }

    return {
      equation,
      display,
      handleNumbers,
      handleAllClear,
      handleDelete,
      handleOperators,
      lastChar,
      handleCalculate,
      includesEqual,
      handleDecimal,
      changeDisplay,
      substractLast,
      maxNumbers,
      isEmpty,
      matchLastOperator,
      matchLastNumber,
      isZero,
      haveOperators,
      divZero,
      includesPeriod,
    };
  },
};
</script>

<style>
.container {
  width: 100%;
  height: 100vh;
}
</style>
