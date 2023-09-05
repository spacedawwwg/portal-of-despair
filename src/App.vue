<script setup lang="ts">
import { ref } from 'vue'

const audio = ref(new Audio())
const playing = ref(false)
const showMore = ref(false)

const sounds = ['despair', 'scream', 'laugh']
const moreSounds = ['chris', 'ronnie', 'nick', 'martin', 'steve']

const play = (sound: string) => {
  playing.value = true
  audio.value = new Audio(`./${sound}.mp3`)
  audio.value.play()
}

const stop = () => {
  playing.value = false
  audio.value.pause()
  audio.value.currentTime = 0
}
</script>

<template>
  <div v-if="!playing" class="options">
    <div class="main">
      <h1>Choose your fear...</h1>
      <button v-for="sound in sounds" :key="sound" @click="play(sound)">
        {{ sound }}
      </button>
    </div>
    <div class="more">
      <button @click="showMore = !showMore" class="more-toggle">
        {{ showMore ? 'Show Less' : 'More...' }}
      </button>
      <div v-if="showMore">
        <button v-for="sound in moreSounds" :key="sound" @click="play(sound)">
          {{ sound }}
        </button>
      </div>
    </div>
  </div>

  <button @click="stop" v-if="playing">Stop it, I'm scared!!!</button>

  <div class="bg"></div>
  <div class="bg bg-2"></div>
  <div class="bg bg-3"></div>
</template>

<style scoped>
.options {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

h1{
  color: #fff;
  margin-bottom: 10px;
  font-size: 1.8rem;
}

button {
  background-color: #ffffff;
  color: #000;
  padding: 10px 20px;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  margin: 10px;
  text-transform: uppercase;
  letter-spacing: 2px;
  outline: none;
  border: solid 3px #fff;
  box-shadow: 20px 38px 34px -26px rgba(0, 0, 0, 0.2);
  border-radius: 255px 15px 225px 15px/15px 225px 15px 255px;
  font-family: slender, san-serif;
}

button:nth-child(1) {
  rotate: 3deg;
}

button:nth-child(3) {
  rotate: -1deg;
}

button:nth-child(4) {
  rotate: 1deg;
}

button:nth-child(5) {
  rotate: -3deg;
}

.main {
  text-align: center;
}

.more {
  text-align: center;
}

.more-toggle {
  border: 0;
  position: fixed;
  bottom: 0;
  left: 0;
  background: none;
  color: #fff;
}
.bg {
  /* animation: slide 3s ease-in-out infinite alternate; */
  background-image: linear-gradient(-60deg, #6ab8b3 50%, #283639 50%);
  bottom: 0;
  left: -50%;
  opacity: 0.5;
  position: fixed;
  right: -50%;
  top: 0;
  z-index: -1;
  filter: blur(100px);
}

.bg-2 {
  animation-direction: alternate-reverse;
  animation-duration: 4s;
}

.bg-3 {
  animation-duration: 5s;
}

@keyframes slide {
  0% {
    transform: translateX(-25%);
  }
  100% {
    transform: translateX(25%);
  }
}
</style>
