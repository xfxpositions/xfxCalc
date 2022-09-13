<template>
  <div class="container">
    <div class="display" :class="{ fit: calc_value?.length > 10 }">
      {{ calc_value || "0" }}
    </div>
    <div class="oprs-wrapper">
      <div class="oprs">
        <template v-for="element in calc_elements">
          <div
            class="btn num"
            :class="{
              'btn-zero': element == '0',
              opr: oprs_right.includes(element),
              'top-opr': ['AC', 'C', '+/-', '%'].includes(element),
            }"
          >
            {{ element }}
          </div>
        </template>
      </div>
    </div>
  </div>
</template>
<script setup>
const calc_elements = [
  "AC",
  "+/-",
  "%",
  "÷",
  "1",
  "2",
  "3",
  "x",
  "4",
  "5",
  "6",
  "-",
  "7",
  "8",
  "9",
  "+",
  "0",
  ",",
  "=",
];
const oprs_right = ["÷", "x", "-", "+", "="];
const calc_value = "0";
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,300;0,400;0,600;1,300;1,400;1,600&display=swap");

*,
*::before,
*::after {
  box-sizing: border-box;
  font-family: "Source Sans Pro", sans-serif;
}

.fit {
  overflow: hidden;
  user-select: none;
  word-wrap: break-word;
  hyphens: auto;
  max-width: fit-content;
}
.container {
  border-radius: 10px;
  overflow: hidden;
  border: 0.5px solid #3f4143;
  -webkit-box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
  box-shadow: 6px 0px 45px -1px rgba(0, 0, 0, 0.75);
  display: inline-flex;
  flex-direction: column;
  max-width: fit-content;
  justify-content: center;
  align-content: center;
}
.display {
  overflow: hidden;
  user-select: none;
  word-wrap: break-word;
  hyphens: auto;
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
.oprs-wrapper {
  max-width: fit-content;
}
.oprs {
  display: grid;
  justify-content: center;
  align-content: center;
  grid-template-columns: repeat(4, 6rem);
  grid-template-rows: repeat(5, 5rem);
  text-align: center;
  border: 1px solid black;
  background-color: azure;
}
.btn {
  font-size: 32px;
  display: flex;
  justify-content: center;
  align-items: center;
  user-select: none;
  border: 1px solid grey;
  color: white;
  background-color: #5f6062;
  border: 1px solid #2b2d2f;
}
.btn:hover {
  background-color: rgb(131, 130, 128) !important;
}
.btn-zero {
  grid-column: 1/3;
}
.btn.opr {
  background-color: #fd9e2b;
  color: #fff0df;
}
.btn.top-opr {
  background-color: #3f4143;
}
</style>
