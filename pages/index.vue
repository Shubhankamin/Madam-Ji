<template>
  <div class="container">
    <div class="bubbling-heart">
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
      <div><i class="fa fa-heart fa-5x"></i></div>
    </div>
    <v-row justify="center">
      <v-col cols="12" sm="8" md="6" lg="4" class="d-flex justify-center">
        <v-card class="text-center card pa-4" elevation="2">
          <v-row class="justify-center">
            <v-col cols="2">
              <v-icon size="60" color="#e8b923">mdi-creation-outline</v-icon>
            </v-col>
          </v-row>
          <v-card-text
            v-if="isFirstTextVisible"
            :class="['text-h5', 'font-weight-bold', 'text-wrap', 'slide-up']"
            class="py-5"
          >
            It's Your Special Day Yeyey!
          </v-card-text>
          <v-card-text
            v-else-if="isSecondTextVisible"
            :class="['text-h5', 'font-weight-bold', 'text-wrap', 'slide-up']"
            class="py-5"
          >
            To Make Something Special For You As You Are Special For Me
          </v-card-text>
          <div v-else-if="isThirdTextVisible" :class="'slide-up'">
            <v-card-text :class="['text-h5', 'font-weight-bold', 'text-wrap']">
              Do You Want To See What I Made For You??
            </v-card-text>
            <div class="d-flex ga-5 justify-center py-5">
              <v-btn class="rounded-xl d-flex align-center btn-no-custom">
                No 😕
              </v-btn>
              <v-btn class="rounded-xl d-flex align-center btn-custom">
                Yes 😉
              </v-btn>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isFirstTextVisible = ref(true);
const isSecondTextVisible = ref(false);
const isThirdTextVisible = ref(false);

onMounted(() => {
  setTimeout(() => {
    isFirstTextVisible.value = false; // Hide first text
    isSecondTextVisible.value = true; // Show second text
  }, 3000); // Change to second text after 3 seconds

  setTimeout(() => {
    isSecondTextVisible.value = false; // Hide second text
    isThirdTextVisible.value = true; // Show third text
  }, 6000); // Change to third text after 6 seconds (3 seconds after the second text appears)
});
</script>

<style scoped>
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css");

body {
  background: deepPink;
  color: #ffc0cb;
  text-shadow: 0 0 40px pink;
}

.btn-custom {
  background: #eeda97; /* Match button color to card's gradient */
  color: #000; /* White text */
  border-radius: 25px; /* Rounded corners */
  transition: background-color 0.3s ease, transform 0.3s ease; /* Smooth transition */
  font-weight: bold;
  padding: 10px 30px;
}

.btn-no-custom {
  background: rgb(206, 62, 62); /* Match button color to card's gradient */
  color: #fff; /* White text */
  border-radius: 25px; /* Rounded corners */
  transition: background-color 0.3s ease, transform 0.3s ease; /* Smooth transition */
  font-weight: bold;
  padding: 10px 30px;
}

.btn-custom:hover {
  background: #ff9a9d; /* Lighter pink for hover effect */
  transform: scale(1.05); /* Slight scale-up effect */
  color: white; /* Reset scale when clicked */
}

.btn-custom:active {
  background: #f8ebe8; /* Soft color when the button is pressed */
  transform: scale(1);
}

.btn-no-custom:hover {
  background: #ff9a9d; /* Lighter pink for hover effect */
  transform: scale(1.05); /* Slight scale-up effect */
  color: black; /* Reset scale when clicked */
}

.btn-no-custom:active {
  background: #f8ebe8; /* Soft color when the button is pressed */
  transform: scale(1); /* Reset scale when clicked */
}

.card {
  position: absolute;
  top: 50%;
  width: 50vw;
  background: linear-gradient(to right, #f8ebe8, #ecd6d0, #ff9a9dbd);
}

.bubbling-heart div {
  position: fixed;
  top: 30%;
  left: 50%;
  transform: translate(-50%, 25vh) scale(0);
  opacity: 0;
  animation: bubbleUp 2s infinite;
}

.bubbling-heart div .fa {
  transform: translateX(19.5vw) rotate(45deg);
  animation: oscillate 4s ease-in-out infinite;
  color: pink;
  text-shadow: 0 0 40px pink;
}

.bubbling-heart div:nth-child(2) {
  animation-delay: 0.5s;
}

.bubbling-heart div:nth-child(2) .fa {
  animation-delay: 1s;
}

.bubbling-heart div:nth-child(3) {
  animation-delay: 1s;
}

.bubbling-heart div:nth-child(3) .fa {
  animation-delay: 1.5s;
}

.bubbling-heart div:nth-child(4) {
  animation-delay: 1.5s;
}

.bubbling-heart div:nth-child(4) .fa {
  animation-delay: 2s;
}

@keyframes bubbleUp {
  50% {
    opacity: 1;
  }
  100% {
    transform: translate(-50%, -25vh) scale(2);
  }
}

@keyframes oscillate {
  50% {
    transform: translateX(-19.5vw) rotate(-25deg);
  }
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
</style>
