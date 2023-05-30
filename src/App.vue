<script setup>
import { ref } from 'vue'

const minute_ = ref(0)
const end_ = ref(6)
const minute = ref(minute_.value)
const end = ref(end_.value)

const timer = ref(null)
const toggle = ref(true)

const start = () => {
  if (minute.value === 0 && end.value <= 0) {
    minute.value = minute_.value
    end.value = end_.value
  }
  toggle.value = !toggle.value
  timer.value = setInterval(() => {
    if (minute.value !== 0 && end.value === 0) {
      minute.value--
      end.value = 59
      return
    }
    end.value--
    if (minute.value === 0 && end.value <= 0) {
      resume()
    }
  }, 1000)
}

const resume = () => {
  clearInterval(timer.value)
  toggle.value = !toggle.value
}

const stop = () => {
  resume()
  minute.value = minute_.value
  end.value = end_.value
}
</script>

<template>
  <div class="wrapper w-full min-h-screen bg-[#F2FFF5]">
    <div class="container mx-auto grid place-items-center h-screen">
      <div class="timer flex flex-col justify-center items-center">
        <div class="status flex items-center gap-[8px] h-[48px]">
          <img src="./assets/img/cup.svg" alt="" />
          <span class="capitalize">short break</span>
        </div>
        <div class="stopwatch">
          <h1>{{ minute.toString().padStart(2, '0') }}</h1>
          <h1>{{ end.toString().padStart(2, '0') }}</h1>
        </div>
        <div class="controls flex gap-3 text-4xl text-[#14401D]">
          <button
            @click="stop"
            class="p-[24px] rounded-[24px] h-20 duration-150 flex justify-center items-center bg-[#e4f9e9]"
          >
            <img src="./assets/img/dots-horizon.svg" alt="" />
          </button>
          <button
            v-if="toggle"
            @click="start"  
            class="pause rounded-3xl duration-150 flex justify-center items-center bg-[#e4f9e9]"
          >
            <i class="bx bx-play"></i>
          </button>
          <button
            v-else
            @click="resume"
            class="pause rounded-3xl duration-150 flex justify-center items-center bg-[#e4f9e9]"
          >
            <i class="bx bx-pause"></i>
          </button>
          <button
            class="p-[24px] rounded-[24px] h-20 duration-150 flex justify-center items-center bg-[#e4f9e9]"
          >
            <img src="./assets/img/skip.svg" alt="" />
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.stopwatch {
  margin: 32px 0;
}
.stopwatch h1 {
  font-size: 256px;
  line-height: 217.6px;
  font-family: 'Roboto Flex';
  font-style: normal;
  font-weight: 800;
  color: #14401d;
}
.status {
  border: 2px solid #471515;
  border-radius: 9999px;
  background: rgba(255, 76, 76, 0.15);
  padding: 8px 16px;
}
.controls {
  height: 200px;
  display: flex;
  align-items: center;
}
.controls button {
  transition: all 0.3s ease;
}
.controls button:hover {
  background-color: #4dda6e9e;
}
.controls .pause {
  align-items: center;
  padding: 32px 48px;
  font-size: 60px;
  width: 128px;
  height: 96px;
  background-color: #4dda6e9e;
}
</style>
