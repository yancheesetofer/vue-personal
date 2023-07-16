<template>
  <div>
    <transition name="fade" mode="out-in">
      <ul class="flex justify-center">
        <li>
          <RouterLink
            to="/"
            class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white dark:text-white"
            v-bind:class="{ 'router-link-active': route === '/' }"
          >
            Home
          </RouterLink>
          <RouterLink
            to="/about"
            class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white dark:text-white"
            v-bind:class="{ 'router-link-active': route === '/about' }"
          >
            About
          </RouterLink>
          <RouterLink
            to="/project"
            class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white dark:text-white"
            v-bind:class="{ 'router-link-active': route === '/project' }"
          >
            Projects
          </RouterLink>
        </li>
      </ul>
    </transition>

    <div>
      <hr class="border-1 my-8 border-gray-400 sm:w-4/12 mx-auto" />
    </div>
  </div>
</template>

<script setup>
import router from "../router";
import { ref, watch } from "vue";

const route = ref(router.currentRoute.value.path);

watch(
  () => router.currentRoute.value.path,
  (newPath) => {
    route.value = newPath;
  }
);
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.router-link-active {
  background-color: rgb(37 99 235 / var(--tw-bg-opacity));
  color: white;
}
</style>
