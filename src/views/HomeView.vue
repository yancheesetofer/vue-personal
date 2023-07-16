<template>
  <div>
    <img
      src="../assets/imgs/profile.jpg"
      class="w-[180px] h-[180px] sm:w-[200px] sm:h-[200px] mx-auto my-auto rounded-full shadow-md"
      alt="profile-picture"
    />
    <h1
      class="mt-8 mb-4 text-center text-3xl sm:text-4xl uppercase font-bold dark:text-white"
    >
      Yan Christofer Silalahi
    </h1>
    <hr class="border-1 my-4 border-gray-400 w-14 mx-auto" />
    <p class="text-center text-xl sm:text-2xl text-gray-700 dark:text-gray-300">
      <span class="typed-text">{{ typeValue }}</span>
      <span class="blinking-cursor">|</span>
      <span class="cursor" :class="{ typing: typeStatus }">&nbsp;</span>
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const displayTextArray = ["<SoftwareEngineer />", "Compsci.tsx", ".achiever"];
const typingSpeed = 100; // Speed of typing in milliseconds
const erasingSpeed = 100; // Speed of erasing in milliseconds
const newTextDelay = 2000; // Delay between words in milliseconds

const typeValue = ref("");
const typeStatus = ref(false);
const displayTextArrayIndex = ref(0);
const charIndex = ref(0);

onMounted(() => {
  setTimeout(typeText, newTextDelay + 200);
});

function typeText() {
  if (charIndex.value < displayTextArray[displayTextArrayIndex.value].length) {
    if (!typeStatus.value) typeStatus.value = true;
    typeValue.value += displayTextArray[displayTextArrayIndex.value].charAt(
      charIndex.value
    );
    charIndex.value += 1;
    setTimeout(typeText, typingSpeed);
  } else {
    typeStatus.value = false;
    setTimeout(eraseText, newTextDelay);
  }
}

function eraseText() {
  if (charIndex.value > 0) {
    if (!typeStatus.value) typeStatus.value = true;
    typeValue.value = displayTextArray[displayTextArrayIndex.value].substring(
      0,
      charIndex.value - 1
    );
    charIndex.value -= 1;
    setTimeout(eraseText, erasingSpeed);
  } else {
    typeStatus.value = false;
    displayTextArrayIndex.value =
      (displayTextArrayIndex.value + 1) % displayTextArray.length;
    setTimeout(typeText, typingSpeed + 1000);
  }
}
</script>

<style scoped>
.typed-text {
  color: #d2b94b;
}

.blinking-cursor {
  font-size: 2rem;
  color: #2c3e50;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  from,
  to {
    color: transparent;
  }
  50% {
    color: #2c3e50;
  }
}

.cursor.typing {
  visibility: hidden;
}
</style>
