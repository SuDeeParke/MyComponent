<!--
 * @Author: sudongpeng sudongpeng@uino.com
 * @Date: 2022-08-12 14:30:19
 * @Description: 组件 屏幕中间部分的 数字
-->
<template>
  <div class="gold-number">
    <p class="number" :style="{ 'font-size': props.numberSize+'px'}">{{ animateNum.num.toLocaleString() }}</p>
    <p class="desc">{{ props.desc }}</p>
  </div>
</template>

<script setup lang="ts">
import * as TWEEN from '@tweenjs/tween.js';

const props = defineProps({
  number: {
    type: Number,
    defalut: 0,
  },
  desc: String,
  numberSize: {
    type: Number,
    default: 150
  },
})


const animateNum = reactive({ num: 0 });
const RAF = ref(-1);
const updateNumber = (newVal: number) => {
  const tween = new TWEEN.Tween(animateNum)
    .to({ num: newVal }, 1500)
    .easing(TWEEN.Easing.Exponential.Out)
    .onUpdate((v) => {
      animateNum.num = Number(v.num.toFixed(0))
    })
    .start()

  const animate = (time?: number) => {
    RAF.value = requestAnimationFrame(animate)
    tween.update(time)
  }
  animate();
}

updateNumber(props.number as number);




watch(() => props.number, (newV) => {
  updateNumber(newV as number);
})



</script>

<style lang="scss" scoped>
.gold-number{
  position: relative;
  text-align: center;
  letter-spacing: 7px;
  .number{
    font-size: 150px;
    font-weight: bold;
    background-image: linear-gradient(to bottom,
        rgba(240, 195, 147, 1) 0%,
        rgba(219, 151, 41, 1) 25%,
        rgb(249, 222, 76, 1) 55%,
        rgba(219, 151, 41, 1) 100%);
    color: transparent;
    background-clip: text;
    -webkit-background-clip: text;
    // text-shadow: 6px 6px 10px rgba($color: #5f5f5f, $alpha: 0.2);
    letter-spacing: 60px;
  }
  .desc {
    font-size:  75px;
    font-weight: bold;
    color: #fff;
  }
}
</style>
