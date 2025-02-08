<template>
  <div class="overflow-hidden">
    <!-- FIRST DIV -->
    <div v-if="isVisible" :class="{ 'dark-background': isDarkMode }">
      <v-row justify="center">
        <v-col cols="12" sm="8" md="6" lg="4" class="d-flex justify-center">
          <v-card
            class="text-center card pa-4"
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
      <div id="balloon-container"></div>
      <v-row>
        <v-col class="pt-14 d-flex flex-column align-center">
          <p class="deco-text">Need Some Balloons ??</p>
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
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isVisible = ref(true); // Controls first div visibility
const isHiding = ref(false);
const showLightsSection = ref(false); // Controls second div visibility
const showDecorations = ref(false); // Controls third div visibility
const isDarkMode = ref(false);
const decoDiv = ref(false);
onMounted(() => {
  setTimeout(() => {
    isHiding.value = true;
    setTimeout(() => {
      isVisible.value = false;
      showLightsSection.value = true; // Show second div after first disappears
    }, 1000); // Matches animation duration
  }, 2000); // Wait 2 seconds before hiding first div
});

const addDeco = () => {
  decoDiv.value = true;
  showDecorations.value = false;
};

const toggleMode = () => {
  isDarkMode.value = !isDarkMode.value;
  document.body.style.backgroundColor = isDarkMode.value
    ? "#212121"
    : "#ffffff";

  // Show third div when switch is toggled
  setTimeout(() => {
    showDecorations.value = true;
    showLightsSection.value = false;
  }, 300);
};

</script>

<style scoped>
.card {
  position: absolute;
  top: 50%;
  width: 50vw;
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
  background-image: url("/images/bday-bg.jpg");
  height: 100vh;
  width: 100vw;
  background-size: cover;
  overflow: hidden !important;
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
</style>
