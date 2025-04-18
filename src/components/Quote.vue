<script setup>
import { ref } from "vue";
import axios from "axios";

const advice = ref(null);
const animate = ref(false);

async function getAdvice() {
  try {
    animate.value = false; // Reset animation
    const { data } = await axios.get("https://api.adviceslip.com/advice");
    console.log("API Data:", data);

    if (data && data.slip) {
      advice.value = data.slip;
      // Trigger animation after setting advice
      setTimeout(() => {
        animate.value = true;
      }, 50);
    } else {
      console.error("Unexpected data structure from API");
    }
  } catch (error) {
    console.error("Error fetching advice:", error);
  }
}
</script>

<template>
  <section class="container">
    <div :class="['card', { shake: animate }]">
      <div v-if="advice" class="title">
        <h4>ADVICE #{{ advice.id }}</h4>
      </div>

      <div v-if="advice" class="text">"{{ advice.advice }}"</div>

      <div class="divider">
        <img src="@/assets/images/pattern-divider-desktop.svg" alt="divider" />
      </div>

      <button @click="getAdvice" class="floating-button">
        <i class="fa-solid fa-dice-five"></i>
      </button>
    </div>
  </section>
</template>

<style scoped>
/* Layout */
.container {
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Card */
.card {
  width: 500px;
  background-color: var(--color-Dark-Grayish-Blue);
  border-radius: 20px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  position: relative;
  text-align: center;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.3);
  transition: transform 0.3s ease;
}

/* Title */
.title h4 {
  color: var(--color-neon-green);
  font-size: 14px;
  letter-spacing: 4px;
  font-family: var(--font-family);
  margin: 0;
}

/* Advice Text */
.text {
  color: var(--color-text);
  font-size: var(--font-size);
  font-weight: var(--font-wights);
  font-family: var(--font-family);
}

/* Divider */
.divider img {
  max-width: 100%;
  margin: 20px 0;
}

/* Button */
.floating-button {
  position: absolute;
  bottom: -25px;
  height: 60px;
  width: 60px;
  border-radius: 50%;
  border: none;
  background-color: var(--color-neon-green);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: box-shadow 0.3s ease;
}

.floating-button i {
  font-size: 28px;
}

.floating-button:hover {
  box-shadow: 0 0 25px hsl(150, 100%, 66%);
}

/* Responsive */
@media screen and (max-width: 414px) {
  .card {
    width: 90%;
    padding: 20px;
  }

  .title h4 {
    font-size: 12px;
  }

  .text {
    font-size: 14px;
  }
}

/* --- Animation --- */

/* Shake animation */
@keyframes shake {
  0% {
    transform: translate(0, 0);
  }
  20% {
    transform: translate(-5px, 0);
  }
  40% {
    transform: translate(5px, 0);
  }
  60% {
    transform: translate(-5px, 0);
  }
  80% {
    transform: translate(5px, 0);
  }
  100% {
    transform: translate(0, 0);
  }
}

/* When "shake" class is added */
.shake {
  animation: shake 0.4s ease;
}
</style>
