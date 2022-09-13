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
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400;1,600&display=swap");
body {
  box-sizing: border-box;
  font-family: "Source Sans Pro", sans-serif;
}
.dummy {
  overflow: auto;
  max-width: 100px;
  max-height: 20px;
  background: #000;
  color: white;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 75vw;
  border-radius: 100px;
}

.app {
  display: grid;
  max-width: 395px;

  border-radius: 10px;
  overflow: hidden;
  border: 0.5px solid #3f4143;
  -webkit-box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
  box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
}
.display {
  overflow: hidden;
  user-select: none;
  min-height: 6rem;
  background-color: #2b2d2f;
  color: white;
  font-size: 56px;

  grid-column: 1 / -1;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  flex-direction: column;
  padding: 10px;
  word-wrap: break-word;
  word-break: break-all;
}
.display-current-opr {
  font-size: 16px;
}
.buttons {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-column-end: 2fr 2fr 2fr;
}
.oprs {
  display: grid;
  grid-template-columns: 1fr;
}
.btn {
  user-select: none;
  min-width: 6rem;
  min-height: 5rem;
  color: #e7e7e7;
  background-color: #5f6062;
  border: 1px solid #2b2d2f;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 32px;
}
.btn.opr {
  box-sizing: border-box;
  background-color: #fd9e2b;
  color: #fff0df;
}
.btn-zero {
  grid-column: 1/3;
}
.btn.top-opr {
  background-color: #3f4143;
}
.selected {
  border: 2px solid black;
}
</style>
