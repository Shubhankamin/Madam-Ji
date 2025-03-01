<template>
  <div class="overflow-x-hidden">
    <!-- FIRST DIV -->
    <div v-if="isVisible" :class="{ 'dark-background': isDarkMode }">
      <v-row justify="center">
        <v-col cols="12" sm="8" md="6" lg="4" class="d-flex justify-center">
          <v-card
            class="text-center card-1 d-none d-md-flex flex-column pa-4"
            :class="{ 'slide-up-leave': isHiding }"
            elevation="2"
          >
            <v-row class="justify-center">
              <v-col cols="2">
                <v-icon size="60" color="#e8b923">mdi-creation-outline</v-icon>
              </v-col>
            </v-row>
            <v-card-text class="text-h5 font-weight-bold text-wrap py-5">
              Have a look at it Madam Jiii!!😌
            </v-card-text>
          </v-card>
          <v-card
            class="text-center card-1-mob d-flex d-md-none flex-column pa-4 mx-10"
            :class="{ 'slide-up-leave': isHiding }"
            elevation="2"
          >
            <v-row class="justify-center">
              <v-col cols="2">
                <v-icon size="60" color="#e8b923">mdi-creation-outline</v-icon>
              </v-col>
            </v-row>
            <v-card-text class="text-h5 font-weight-bold text-wrap py-5">
              Have a look at it Madam Jiii!!😌
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </div>

    <!-- SECOND DIV (Lights Section) -->
    <div v-if="showLightsSection" class="dark-background">
      <v-row class="justify-center">
        <v-col cols="12" class="d-flex flex-column align-center pt-14">
          <p class="light-text">
            {{ "Turn On Lights" }}
          </p>

          <!-- Switch Button -->
          <label class="switch">
            <input class="cb" type="checkbox" @change="toggleMode" />
            <span class="toggle">
              <span class="left">off</span>
              <span class="right">on</span>
            </span>
          </label>
        </v-col>
      </v-row>
    </div>

    <!-- THIRD DIV (Decorations Section) -->
    <div v-if="showDecorations" class="bg-white">
      <v-row>
        <v-col class="pt-14 d-flex flex-column align-center">
          <p class="deco-text">Add Decorations</p>
          <label class="switch" @click="addDeco">
            <input type="checkbox" class="checkbox" />
            <div class="slider"></div>
          </label>
        </v-col>
      </v-row>
    </div>

    <!-- FOURTH DIV (Background Image) -->
    <div v-if="decoDiv" class="deco">
      <!-- Balloon row 1 -->
      <v-row
        class="justify-space-between px-16 mx-10 d-none d-md-flex"
        :class="{ 'fade-in': showBalloons, hidden: !showBalloons }"
      >
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png" lazy-src="/images/balloon-1.png"></v-img>
        </v-col>
        <v-col cols="12" md="3">
          <v-img src="/images/birthday-text.png" lazy-src="/images/birthday-text.png"></v-img>
        </v-col>
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png" lazy-src="/images/balloon-1.png"></v-img>
        </v-col>
      </v-row>
      <v-row
        class="justify-center d-flex d-md-none"
        :class="{ 'fade-in': showBalloons, hidden: !showBalloons }"
      >
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png" lazy-src="/images/balloon-1.png"></v-img>
        </v-col>
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png" lazy-src="/images/balloon-1.png"></v-img>
        </v-col>
        <v-col cols="8" md="3">
          <v-img src="/images/birthday-text.png" lazy-src="/images/balloon-1.png"></v-img>
        </v-col>
      </v-row>
      <v-row v-if="!showBalloons">
        <v-col class="pt-10 d-flex flex-column align-center">
          <p class="deco-text">Add Some Balloons ??</p>
          <div>
            <button class="cta" @click="addBalloons">
              <span>Add</span>
              <svg width="15px" height="10px" viewBox="0 0 13 10">
                <path d="M1,5 L11,5"></path>
                <polyline points="8 1 12 5 8 9"></polyline>
              </svg>
            </button>
          </div>
        </v-col>
      </v-row>

      <v-row v-if="showAudio">
        <v-col class="d-flex justify-center">
          <div class="d-flex flex-column align-center">
            <p class="deco-text">Play Music</p>
            <div class="volume" @click="playMusic" :class="'fade-in'">
              <input type="checkbox" class="volume-input" />
              <div class="volume-icon">
                <svg
                  viewBox="0 0 24 24"
                  width="24"
                  height="24"
                  stroke="currentColor"
                  stroke-width="2"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="volume-svg"
                >
                  <polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>
                  <path
                    d="M19.07 4.93a10 10 0 0 1 0 14.14M15.54 8.46a5 5 0 0 1 0 7.07"
                  ></path>
                </svg>
              </div>
            </div>
          </div>
        </v-col>
      </v-row>

      <v-row v-if="showPics">
        <v-col
          v-for="(pic, index) in pics"
          :key="index"
          :class="[
            'd-flex justify-center',
            { 'fade-in': showPics },
            { 'mt-md-16 pt-md-10': index === 1 || index === pics.length - 1 }, // Apply mt-16 and pt-10 to the second and last cards
          ]"
        >
          <div class="card">
            <v-img :src="pic.src" cover :lazy-src="pic.src"></v-img>
            <div class="card__content">
              <p class="card__description">{{ pic.description }}</p>
            </div>
          </div>
        </v-col>
      </v-row>
      <!-- Balloon row 2 -->

      <v-row
        class="justify-space-between px-md-16 mx-md-10"
        :class="{ 'fade-in': showBalloons, hidden: !showBalloons }"
      >
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png"></v-img>
        </v-col>
        <v-col cols="6" md="3">
          <v-img src="/images/balloon-1.png"></v-img>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

// States
const isVisible = ref(true);
const isHiding = ref(false);
const showLightsSection = ref(false);
const showDecorations = ref(false);
const isDarkMode = ref(false);
const decoDiv = ref(false);
const showBalloons = ref(false);
const showAudio = ref(false);
let audio; // Declare audio outside of refs
const showPics = ref(false);

onMounted(() => {
  // Initialize audio on mounted lifecycle hook
  audio = new Audio("/audio/bl-aud.mp3");

  setTimeout(() => {
    isHiding.value = true;
    setTimeout(() => {
      isVisible.value = false;
      showLightsSection.value = true; // Show second div after first disappears
    }, 1000);
  }, 2000); // Wait 2 seconds before hiding first div
});

// Play music function
const playMusic = () => {
  audio.play();
  showAudio.value = false;
  setTimeout(() => {
    showPics.value = true; // Start showing the pictures after some time
  }, 800);
};

const addDeco = () => {
  decoDiv.value = true;
  showDecorations.value = false;
};

const addBalloons = () => {
  showBalloons.value = true;
  showAudio.value = true; // Show balloons when button is clicked
};

const toggleMode = () => {
  isDarkMode.value = !isDarkMode.value;
  document.body.style.backgroundColor = isDarkMode.value
    ? "#212121"
    : "#ffffff";

  setTimeout(() => {
    showDecorations.value = true;
    showLightsSection.value = false;
  }, 300);
};

const pics = [
  {
    src: "/images/her1.jpg",
    description: "Happy Birthday to the most fantabulous amazing beautiful woman in the whole universe/multiverse",
  },
  {
    src: "/images/her-6.jpeg",
    description: "I wish you a lots and lots of happiness, love and success. Hope everything that you've dreamed of come true",
  },
  {
    src: "/images/her-4.jpg",
    description: "On this day I hope you know how amazing you are how you light up the world and with kindness",
  },
  {
    src: "/images/her-7.jpeg",
    description: "Lastly thank you for everything I hope you don't stop kaleshi with me forever and ever ukwim. Wishing you lots of love again happy Birthday!. I love you",
  },
];
</script>

<style scoped>
:root {
  --gps-burg: rgba(182, 15, 97, 0.9);
  --gps-orange: rgba(242, 112, 45, 0.9);
  --gps-skyblue: rgba(45, 181, 167, 0.9);
  --gps-purple: rgba(190, 61, 244, 0.9);
  --gps-green: rgba(180, 224, 67, 0.9);
  --gps-yellow: rgba(242, 194, 58, 0.9);
}
.card-1 {
  position: absolute;
  top: 50%;
  width: 50vw;
  background: linear-gradient(to right, #f8ebe8, #ecd6d0, #ff9a9dbd);
}

.card-1-mob {
  position: absolute;
  top: 50%;
  background: linear-gradient(to right, #f8ebe8, #ecd6d0, #ff9a9dbd);
}

.slide-up {
  animation: slideUp 1s ease-out;
}

@keyframes slideUp {
  0% {
    transform: translateY(20px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

.slide-up-leave {
  animation: slideUpDisappear 1s ease-out forwards;
}

/* Keyframe for slide-up hide effect */
@keyframes slideUpDisappear {
  0% {
    transform: translateY(0);
    opacity: 1;
  }
  100% {
    transform: translateY(-20px);
    opacity: 0;
  }
}

/* Dark Background Effect */
.dark-background {
  background-color: #212121 !important; /* Dark grey */
  color: white !important; /* Change text color for better visibility */
  height: 100vh; /* Cover full viewport */
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  transition: background-color 1s ease-in-out; /* Smooth transition */
}

.fade-in {
  opacity: 1;
  transform: scale(1);
  transition: opacity 0.7s ease-in-out, transform 0.7s ease-in-out;
}

/* Initially hidden state for balloons */
.hidden {
  opacity: 0;
  transform: scale(0.8);
}

/* Text Above the Button */
.light-text {
  color: antiquewhite;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
}

.deco-text {
  color: #000;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin-bottom: 10px;
}

/* Button Styling */
.container {
  width: 7em;
  height: 7em;
  position: relative;
}

.button {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  border: 4px solid #090909;
  background-color: transparent;
  background-image: linear-gradient(145deg, #171717, #444245);
  box-sizing: border-box;
  box-shadow: inset 2px 2px 0 #7d7c7e, inset -2px -2px 0px #1c1c1c;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.container input {
  display: none;
}

.button::before {
  position: absolute;
  content: "";
  width: 7.25em;
  height: 7.25em;
  border-radius: inherit;
  background-color: transparent;
  background-image: linear-gradient(145deg, #262626, #606060);
  z-index: -1;
  box-shadow: 11px 11px 22px #141414, -11px -11px 22px #525252;
}

.button .icon {
  width: 60px;
  height: 60px;
  display: inline-block;
}

.button .icon svg {
  height: 100%;
  width: 100%;
  fill: #a5a5a5;
}

.container input:checked + .button {
  box-shadow: inset -2px -2px 0 #5e5e5e, inset 2px 2px 0 #1c1c1c;
  border: 4px solid rgb(0, 215, 0);
  animation: animeBorder 0.3s linear alternate-reverse infinite;
}

.container input:checked + .button .icon svg {
  fill: rgb(0, 215, 0);
  animation: animeFill 0.3s linear alternate-reverse infinite;
}

@keyframes animeFill {
  to {
    fill: rgba(0, 194, 0, 0.954);
  }
}

@keyframes animeBorder {
  to {
    border-color: rgba(0, 175, 0, 0.878);
  }
}

.background-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  transition: background-color 0.5s ease-in-out;
}

/* Dark Mode */
.dark {
  background-color: #222;
  color: white;
  animation: slideUp 0.8s ease-in-out forwards;
}

/* Light Mode */
.light {
  background-color: white;
  color: black;
  animation: slideDown 0.8s ease-in-out forwards;
}

/* Slide Up (Dark Mode) */
/* @keyframes slideUp {
  from {
    transform: translateY(100%);
  }
  to {
    transform: translateY(0);
  }
} */

/* Slide Down (Light Mode) */
/* Slide-down effect when showing */
.slide-down-enter {
  animation: slideDownAppear 1s ease-out forwards;
}

/* Keyframe for slide-down show effect */
@keyframes slideDownAppear {
  0% {
    transform: translateY(-20px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

/* From Uiverse.io by r7chardgh */
/* The switch - the box around the slider */
.switch {
  font-size: 17px;
  position: relative;
  display: inline-block;
  width: 5em;
  height: 2.5em;
  user-select: none;
}

/* Hide default HTML checkbox */
.switch .cb {
  opacity: 0;
  width: 0;
  height: 0;
}

/* The slider */
.toggle {
  position: absolute;
  cursor: pointer;
  width: 100%;
  height: 100%;
  background-color: #373737;
  border-radius: 0.1em;
  transition: 0.4s;
  text-transform: uppercase;
  font-weight: 700;
  overflow: hidden;
  box-shadow: -0.3em 0 0 0 #373737, -0.3em 0.3em 0 0 #373737,
    0.3em 0 0 0 #373737, 0.3em 0.3em 0 0 #373737, 0 0.3em 0 0 #373737;
}

.toggle > .left {
  position: absolute;
  display: flex;
  width: 50%;
  height: 88%;
  background-color: #f3f3f3;
  color: #373737;
  left: 0;
  bottom: 0;
  align-items: center;
  justify-content: center;
  transform-origin: right;
  transform: rotateX(10deg);
  transform-style: preserve-3d;
  transition: all 150ms;
}

.left::before {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  background-color: rgb(206, 206, 206);
  transform-origin: center left;
  transform: rotateY(90deg);
}

.left::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  background-color: rgb(112, 112, 112);
  transform-origin: center bottom;
  transform: rotateX(90deg);
}

.toggle > .right {
  position: absolute;
  display: flex;
  width: 50%;
  height: 88%;
  background-color: #f3f3f3;
  color: rgb(206, 206, 206);
  right: 1px;
  bottom: 0;
  align-items: center;
  justify-content: center;
  transform-origin: left;
  transform: rotateX(10deg) rotateY(-45deg);
  transform-style: preserve-3d;
  transition: all 150ms;
}

.right::before {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  background-color: rgb(206, 206, 206);
  transform-origin: center right;
  transform: rotateY(-90deg);
}

.right::after {
  position: absolute;
  content: "";
  width: 100%;
  height: 100%;
  background-color: rgb(112, 112, 112);
  transform-origin: center bottom;
  transform: rotateX(90deg);
}

.switch input:checked + .toggle > .left {
  transform: rotateX(10deg) rotateY(45deg);
  color: rgb(206, 206, 206);
}

.switch input:checked + .toggle > .right {
  transform: rotateX(10deg) rotateY(0deg);
  color: #487bdb;
}

/* From Uiverse.io by Galahhad */
.checkbox {
  display: none;
}

.slider {
  width: 60px;
  height: 30px;
  background-color: lightgray;
  border-radius: 20px;
  overflow: hidden;
  display: flex;
  align-items: center;
  border: 4px solid transparent;
  transition: 0.3s;
  box-shadow: 0 0 10px 0 rgb(0, 0, 0, 0.25) inset;
  cursor: pointer;
}

.slider::before {
  content: "";
  display: block;
  width: 100%;
  height: 100%;
  background-color: #fff;
  transform: translateX(-30px);
  border-radius: 20px;
  transition: 0.3s;
  box-shadow: 0 0 10px 3px rgb(0, 0, 0, 0.25);
}

.checkbox:checked ~ .slider::before {
  transform: translateX(30px);
  box-shadow: 0 0 10px 3px rgb(0, 0, 0, 0.25);
}

.checkbox:checked ~ .slider {
  background-color: #2196f3;
}

.checkbox:active ~ .slider::before {
  transform: translate(0);
}

.deco {
  background-image: url("/images/bday-bg-2.jpg");
  height: 100vh;
  width: 100vw;
  background-size: cover;
  overflow-x: hidden !important;
  z-index: -1;
  
}

/* From Uiverse.io by alexmaracinaru */
.cta {
  position: relative;
  margin: auto;
  padding: 12px 18px;
  transition: all 0.2s ease;
  border: none;
  background: none;
  cursor: pointer;
}

.cta:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  border-radius: 50px;
  background: #b1dae7;
  width: 45px;
  height: 45px;
  transition: all 0.3s ease;
}

.cta span {
  position: relative;
  font-family: "Ubuntu", sans-serif;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 0.05em;
  color: #234567;
}

.cta svg {
  position: relative;
  top: 0;
  margin-left: 10px;
  fill: none;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke: #234567;
  stroke-width: 2;
  transform: translateX(-5px);
  transition: all 0.3s ease;
}

.cta:hover:before {
  width: 100%;
  background: #b1dae7;
}

.cta:hover svg {
  transform: translateX(0);
}

.cta:active {
  transform: scale(0.95);
}

/* body {
  margin: 0;
} */

#balloon-container {
  height: 100vh;
  padding: 1em;
  box-sizing: border-box;
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
  transition: opacity 500ms;
}

.balloon {
  height: 125px;
  width: 105px;
  border-radius: 75% 75% 70% 70%;
  position: relative;
}

.balloon:before {
  content: "";
  height: 75px;
  width: 1px;
  padding: 1px;
  background-color: #fdfd96;
  display: block;
  position: absolute;
  top: 125px;
  left: 0;
  right: 0;
  margin: auto;
}

.balloon:after {
  content: "▲";
  text-align: center;
  display: block;
  position: absolute;
  color: inherit;
  top: 120px;
  left: 0;
  right: 0;
  margin: auto;
}

@keyframes float {
  from {
    transform: translateY(100vh);
    opacity: 1;
  }
  to {
    transform: translateY(-300vh);
    opacity: 0;
  }
}

.box-canvas {
  position: relative;
  margin: auto;
  display: block;
  margin-bottom: 8%;
  width: 230px;
  height: 600px;
  animation: floatUp 5s infinite linear;
}
.box-canvas-2 {
  position: relative;
  margin: auto;
  display: block;
  margin-bottom: 8%;
  width: 230px;
  height: 600px;
  animation: floatUp 10s infinite linear;
}

.box-canvas-3 {
  position: relative;
  margin: auto;
  display: block;
  margin-bottom: 8%;
  width: 230px;
  height: 600px;
  margin-left: 60px;
  animation: floatUp 5s infinite linear;
}

.box-canvas-4 {
  position: relative;
  margin: auto;
  display: block;
  margin-bottom: 8%;
  width: 230px;
  height: 600px;
  margin-left: 70px;
  animation: floatUp 5s infinite linear;
}

@keyframes floatUp {
  0% {
    transform: translateY(100vh);
  }

  100% {
    transform: translateY(-480px);
  }
}

.red {
  --balloon-color: var(--red);
  --highlight-color: #fc9999;
  --top-initial: 40px;
  --string-angle: -20deg;
}

.yellow {
  --balloon-color: #f2f24b;
  --highlight-color: #e5e570;
  --top-initial: 80px;
  --left-initial: 50px;
  --string-angle: -8deg;
}

.green {
  --balloon-color: var(--green);
  --highlight-color: #bad6d3;
  --top-initial: 0;
  --left-initial: 80px;
  --string-angle: 1deg;
}

.blue {
  --balloon-color: dodgerblue;
  --highlight-color: #6ab5fc;
  --left-initial: 100px;
  --top-initial: 110px;
  --string-angle: 10deg;
}

.orange {
  --balloon-color: orange;
  --highlight-color: #f9b94a;
  --left-initial: 140px;
  --top-initial: 50px;
  --string-angle: 18deg;
}

.balloon-wrapper {
  position: absolute;
  left: var(--left-initial);
  top: var(--top-initial);
  width: 85px;
}

.string {
  position: absolute;
  top: 110px;
  left: 42px;
  transform: rotate(var(--string-angle));
  transform-origin: top left;
  width: 2px;
  height: 250px;
  background: #50535e;
}

.balloon {
  position: absolute;
  width: 85px;
  height: 100px;
  background: var(--balloon-color);
  border-radius: 50%;
}

.balloon::before {
  content: "";
  position: absolute;
  right: 20px;
  top: 15px;
  width: 15px;
  height: 35px;
  box-shadow: 5px 0 0 var(--highlight-color);
  border-radius: 50%;
  transform: rotate(-30deg);
}

.balloon::after {
  content: "";
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  bottom: -15px;
  width: 25px;
  height: 20px;
  background: var(--balloon-color);
  clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);
}

/* From Uiverse.io by barisdogansutcu */
.volume {
  width: 60px;
  height: 60px;
  border-radius: 100%;
  background-color: rgb(205, 191, 247);
  overflow: hidden;
  position: relative;
}
.volume-icon {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.5s ease;
  overflow: hidden;
  position: relative;
}
.volume-input {
  position: absolute;
  inset: 0;
  opacity: 0;
  cursor: pointer;
  z-index: 999;
}
.volume-icon:before {
  content: "";
  display: flex;
  width: 0px;
  height: 0px;
  border-radius: 100%;
  transition: all 0.2s ease;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background-color: rgb(32, 33, 36);
}
.volume-input:checked + .volume-icon:before {
  width: calc(100% + 4px);
  height: calc(100% + 4px);
}
.volume-svg {
  z-index: 2;
  color: rgb(32, 33, 36);
  height: 30px;
  width: 30px;
}
.volume-input:checked + .volume-icon svg {
  color: rgb(255, 255, 255);
}

/* From Uiverse.io by gharsh11032000 */
.card {
  position: relative;
  width: 300px;
  height: 200px;
  background-color: #f2f2f2;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  perspective: 1000px;
  box-shadow: 0 0 0 5px #ffffff80;
  transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
}

.card svg {
  width: 48px;
  fill: #333;
  transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 16px rgba(255, 255, 255, 0.2);
}

.card__content {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  padding: 20px;
  box-sizing: border-box;
  background-color: #f2f2f2;
  transform: rotateX(-90deg);
  transform-origin: bottom;
  transition: all 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.card:hover .card__content {
  transform: rotateX(0deg);
}

.card__title {
  margin: 0;
  font-size: 24px;
  color: #333;
  font-weight: 700;
}

.card:hover svg {
  scale: 0;
}

.card__description {
  margin: 10px 0 0;
  font-size: 16px;
  color: #777;
  line-height: 1.4;
}

.fade-in-new {
  opacity: 0;
  transform: translateY(20px);
  animation: fadeInUp 0.9s ease-in-out;
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
