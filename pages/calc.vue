<template>
  <body>
    <div class="container">
      <div class="app">
        <div class="display">
          <span class="display-current-opr">{{
            `${display_prev} ${display_prev && selectedOpr}`
          }}</span>
          <span class="display-text">{{ display }}</span>
        </div>
        <div style="display: flex">
          <div class="buttons">
            <div class="btn top-opr" @click="cleanAll">
              {{ display == "0" || !display ? "AC" : "C" }}
            </div>
            <div class="btn top-opr">+/-</div>
            <div class="btn top-opr">%</div>
            <template v-for="value in 9">
              <div class="btn" @click="append(value)">{{ value }}</div>
            </template>
            <div class="btn btn-zero">0</div>
            <div class="btn">,</div>
          </div>
          <div class="oprs">
            <div
              v-for="opr in oprs"
              @click="selectOpr(opr.text)"
              :class="{ selected: selectedOpr == opr }"
              class="btn opr"
            >
              {{ opr.symbol }}
            </div>
            <div class="btn opr">=</div>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>
<script setup>
import { ref, watch } from "vue";

const display = ref("0");
const display_prev = ref("");

const oprs = [
  { symbol: "÷", text: "/" },
  { symbol: "x", text: "*" },
  { symbol: "-", text: "-" },
  { symbol: "+", text: "+" },
];
const selectedOpr = ref("");
const process = ref([]);
const _contually_calculate_exception = ref(false);

const cleanAll = () => {
  display.value = "0";
  display_prev.value = "";
  process.value = [];
};
const selectOpr = (opr) => {
  selectedOpr.value = opr;
  display_prev.value = display.value;
  process.value.push(display_prev.value);
  if (process.value[1] == opr && _contually_calculate_exception) {
    calculate(false);
    _contually_calculate_exception.value = true;
  }

  process.value.push(opr);
  console.log(process.value);
};
const append = (value) => {
  if (display.value === "0") {
    display.value = "";
  }

  if (display_prev.value == display.value) {
    display.value = "";
  }
  display.value += String(value);
};

const calculate = (complete) => {
  const total = eval(process.value.join(" "));
  if (complete) {
    display.value = total;
  } else {
    display_prev.value = total;
    display.value = total;
  }
};

watch(process, (value, prevValue) => {
  console.log(value);
});
</script>
