<template>
  <div class="app" ref="app">
    <div class="display">
      <div class="previous-opr"></div>
      <div class="current-opr">123</div>
    </div>
    <div class="btns-num">
      <button v-for="i in 9" class="btn num">{{ i }}</button>
    </div>

    <div class="btn btn-zero">0</div>
    <div class="oprs">
      <button class="btn opr">÷</button>
      <button class="btn opr">×</button>
      <button class="btn opr">-</button>
      <button class="btn opr">+</button>
      <button class="btn opr">=</button>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
const app = ref(null);
const appWidth = ref("");
onMounted(() => {
  console.log(app.value);
  appWidth.value = app.value.clientWidth;
  console.log(appWidth);
});
</script>
