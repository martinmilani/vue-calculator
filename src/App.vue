<template>
  <div class="flex items-center justify-center h-screen bg-gray-200">
    <div class="w-80 bg-white rounded-xl overflow-hidden shadow-2xl">
      <Display :equation="equation" :display="display" />
      <Board :handleNumbers="handleNumbers" />
    </div>
  </div>
</template>

<script>
import Display from "./components/Display";
import Board from "./components/Board";
import { ref } from "vue";

export default {
  components: { Display, Board },
  setup() {
    const equation = ref("");
    const display = ref("0");

    function handleNumbers(e) {
      if (display.value.length <= 9) {
        if (equation.value.match(/[0-9.]$/) && !equation.value.includes("=")) {
          if (equation.value.match(/[+\-*/]/) == null) {
            let val = equation.value + e.currentTarget.value;
            display.value = val;
            equation.value = val;
          } else {
            display.value(display.value + e.currentTarget.value);
            equation.value(equation.value + e.currentTarget.value);
          }
        } else {
          if (equation.value.match(/[+\-*/]$/)) {
            let val =
              <equation class="value"></equation> + e.currentTarget.value;
            display.value = e.currentTarget.value;
            equation.value = val;
          } else {
            if (
              (display.value === "0" && e.currentTarget.value !== "0") ||
              equation.value.includes("=")
            ) {
              equation.value = e.currentTarget.value;
              display.value = e.currentTarget.value;
              console.log(display.value);
              console.log(equation.value);
            }
          }
        }
      } else {
        window.alert("Max - 10 digits!");
      }
    }

    return {
      equation,
      display,
      handleNumbers,
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
