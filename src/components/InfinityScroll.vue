<template>
  <div class="infinity-scroll">
    <div class="wrap">
      <ul class="list">
        <li class="card" v-for="(item, index) in 5" :key="`${item}_${index}`">
          {{item}}
        </li>
        <li class="card" v-for="(item, index) in 5" :key="`${item}_${index}`">
          {{item}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

$gap: 20px;
$cardWidth: 500px;
.infinity-scroll {
  position: relative;
  width: 800px;
  height: 200px;
  .wrap{
    position: relative;
    display: block;
    width: 100%;
    height: 100%;
    overflow-x: auto;
    overflow-y: hidden;
    border-radius: 10px;
    border: 1px solid #232323;
    box-shadow:
        2.8px 2.8px 2.2px rgba(0, 0, 0, 0.02),
        6.7px 6.7px 5.3px rgba(0, 0, 0, 0.028),
        12.5px 12.5px 10px rgba(0, 0, 0, 0.035),
        22.3px 22.3px 17.9px rgba(0, 0, 0, 0.042),
        41.8px 41.8px 33.4px rgba(0, 0, 0, 0.05),
        100px 100px 80px rgba(0, 0, 0, 0.07);
    &::-webkit-scrollbar{
      display: none;
    }
    .list{
      position: absolute;
      left: 0px;
      top: 0px;
      display: flex;
      width: auto;
      height: 100%;
      gap: 20px;
      background-color: rgb(163, 163, 163);
      border-radius: 10px;
      padding: 20px;
      animation: 50s linear infinite scrollAnimation;
      .card{
        display: block;
        width: $cardWidth;
        height: 100%;
        background: #e0e0e0;
        border-radius: 10px;
        font-size: 80px;
        line-height: 80px;
        padding: 10px;
        color: #232323;
      }
    }
  }
}

@keyframes scrollAnimation {
  from {
    left: 0px;
  }
  to {
    left: -($cardWidth + $gap) * 5;
  }
}
</style>