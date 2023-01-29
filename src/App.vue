<template>
  <div class="main">
    <div class="title">Input</div>
    <!-- <img src="@/assets/test.png" alt=""> -->
    <div class="input_val">
      <span class="box" :style="{ background: background }"></span>
      <input class="text" type="text" :value="background" @change="changeColor" />
      <span class="arrow" :class="{ active: isOpen }" @click="openColors">></span>
    </div>
    <div class="all_color" v-if="isOpen">
      <AppButton v-for="color in AllColor" :key="color" :color="color" @choose="chooseColor" />
    </div>
    <div class="title">Output</div>
    <button class="output_btn" :style="{ bordeColor: textcolor, color: textcolor, background: background }">
      {{ background }}
    </button>
  </div>
</template>
<script setup>
import AppButton from "@/components/AppButton.vue"
import { ref, reactive, computed } from "vue";
let background = ref("#00ff00")
let isOpen = ref(false)
let textcolor = ref("#000000")
let AllColor = reactive([
  "#000000",
  "#013600",
  "#006600",
  "#009d05",
  "#13c302",
  "#01ff01",
  "#3c0000",
  "#323303",
  "#326601",
  "#3a8c03",
  "#34cb02",
  "#32fe02",
  "#6b0000",
  "#663301",
  "#656504",
  "#69c904",
  "#64fe01",
  "#010035",
  "#043035",
  "#026534",
  "#059734",
  "#00d030",
  "#01fe31",
  "#2d032e",
  "#343236",
  "#356433",
  "#39943c",
  "#3dc640",
  "#34cc34",
  "#34fe35",
  "#650135",
  "#683232",
  "#656633",
  "#69982d",
  "#63d02e",
  "#ffffff",
])
let openColors = () => {
  isOpen.value = !isOpen.value
}
let chooseColor = (color) => {
  background.value = color;
  getTextColor(color)
}
let getTextColor = (color) => {
  let r = parseInt(color[1]+color[2], 16), g = parseInt(color[3]+color[4], 16), b = parseInt(color[5]+color[6], 16);
  let max = Math.max(r, g, b), min = Math.min(r, g, b);
  let h, s, l = (max + min) / 2;
  if(l/255>=0.5){
    textcolor.value="#000000"
  }else{
    textcolor.value="#ffffff"
  }
  // if (max == min) {
  //   h = s = 0;
  // } else {
  //   let d = max - min;
  //   s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
  //   switch (max) {
  //     case r: h = (g - b) / d + (g < b ? 6 : 0); break;
  //     case g: h = (b - r) / d + 2; break;
  //     case b: h = (r - g) / d + 4; break;
  //   }
  //   h /= 6;
  // }
  // H - цветовой тон, S - насыщенность, L - светлота [h, s, l]
}
let changeColor = (e) => {
  if (validat(e.target.value)) {
    background.value = e.target.value;
    getTextColor(e.target.value)
  }
}
let validat = (color) => {
  if(color[0]!="#"){
    alert("Значение должно начаться '#'")
    return false
  }else if(color.length!=7){
    alert("Значение должно быть минимум 7 значений")
    return false
  }else if(isNaN(parseInt(color[1], 16))  || isNaN(parseInt(color[2], 16)) || isNaN(parseInt(color[3], 16)) || isNaN(parseInt(color[4], 16)) || isNaN(parseInt(color[5], 16)) || isNaN(parseInt(color[6], 16)) ||  isNaN(parseInt(color[6], 16))){
    alert("Значение должно быть от 0 до F ")
    return false
  }else{
    return true
  }
}
</script>
<style lang="scss" scoped>
.main {
  text-align: center;

  .box {
    border: 1px solid;
    display: inline-block;
    width: 20px;
    height: 20px;
  }

  .all_color {
    width: 360px;
    display: flex;
    align-items: center;
    justify-content: start;
    flex-wrap: wrap;
    margin: auto;
  }

  .input_val {
    padding: 10px 20px;
    border: 1px solid;
    display: flex;
    width: 220px;
    align-items: center;
    border-radius: 5px;
    margin: auto;
    margin-bottom: 10px;
    justify-content: space-around;
    cursor: pointer;

    .box {
      margin-right: 5px;
    }

    .arrow {
      font-size: 1.2rem;
      transform: rotate(90deg);

      &.active {
        transform: rotate(-90deg);
      }
    }
  }

  .output_btn {
    padding: 10px 20px;
    font-size: 1.5rem;
  }
}
</style>
