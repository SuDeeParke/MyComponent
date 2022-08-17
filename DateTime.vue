<template>
    <div class="time-group">
        <!-- 年月日 -->
        <span>{{ year }}-{{ fixZero(transformMonth) }}-{{ fixZero(date) }}</span>
        <!-- 星期 -->
        <span>{{ matchDay(day) }}</span>
        <!-- 时间 -->
        <span>{{ fixZero(hour) }}</span>
        <span class="flash">:</span>
        <span>{{ fixZero(minute) }}</span>
        <span class="flash">:</span>
        <span>{{ fixZero(seconds) }}</span>
    </div>
</template>

<script setup>
const time = new Date()

const year = ref(time.getFullYear())
const month = ref(time.getMonth())
const date = ref(time.getDate())
const day = ref(time.getDay())
const hour = ref(time.getHours())
const minute = ref(time.getMinutes())
const seconds = ref(time.getSeconds())

const transformMonth = computed(() => month.value + 1)

const matchDay = (num) => {
    switch (num) {
        case 0:
            return '星期日'
        case 1:
            return '星期一'
        case 2:
            return '星期二'
        case 3:
            return '星期三'
        case 4:
            return '星期四'
        case 5:
            return '星期五'
        case 6:
            return '星期六'
        default:
            return ''
    }
}

const fixZero = (num) => {
    if (num < 10) {
        return `0${num}`
    }
    return `${num}`
}

const updateDate = () => {
    const newTime = new Date()
    year.value = newTime.getFullYear()
    month.value = newTime.getMonth()
    date.value = newTime.getDate()
    day.value = newTime.getDay()
    hour.value = newTime.getHours()
    minute.value = newTime.getMinutes()
    seconds.value = newTime.getSeconds()
}

let timer

onMounted(() => {
    timer = setInterval(() => {
        updateDate()
    }, 1000)
})

onUnmounted(() => {
    if (timer) {
        clearInterval(timer)
    }
})

</script>

<style lang="scss" scoped>
.time-group {
  font-size: 62px;
  line-height: 62px;
  height: 62px;
  margin-top: -5px;
  font-family: DINPro-Medium;
  font-weight: 500;
  color: #F4F9FF;

  >span {
    &:nth-of-type(1) {
      margin-right: 50px;
    }

    &:nth-of-type(2) {
      margin-right: 40px;
    }
  }
}

.flash {
  position: relative;
  top: -5px;
}
</style>
