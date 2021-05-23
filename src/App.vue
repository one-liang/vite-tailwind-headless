<template>
  <div class="py-16">
    <Switch
      v-model="enabled"
      :class="enabled ? 'bg-blue-500' : 'bg-blue-300'"
      class="relative inline-flex flex-shrink-0 h-[38px] w-[74px] border-2 border-transparent rounded-full cursor-pointer transition-colors ease-in-out duration-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75"
    >
      <span class="sr-only">Use setting</span>
      <span
        aria-hidden="true"
        :class="enabled ? 'translate-x-9' : 'translate-x-0'"
        class="pointer-events-none inline-block h-[34px] w-[34px] rounded-full bg-white shadow-lg transform ring-0 transition ease-in-out duration-200"
      />
    </Switch>
  </div>
  <MyModal />
  <div class="flex flex-col items-center py-16">
    <div class="w-32 h-32">
      <TransitionRoot
        appear
        :show="isShowing"
        as="template"
        enter="transform transition duration-[400ms]"
        enter-from="opacity-0 rotate-[-120deg] scale-50"
        enter-to="opacity-100 rotate-0 scale-100"
        leave="transform duration-200 transition ease-in-out"
        leave-from="opacity-100 rotate-0 scale-100 "
        leave-to="opacity-0 scale-95 "
      >
        <div class="w-full h-full bg-gray-500 rounded-md shadow-lg" />
      </TransitionRoot>
    </div>
    <button
      @click="resetIsShowing"
      class="flex items-center px-3 py-2 mt-8 text-sm font-medium text-white transition transform bg-black rounded-full active:bg-opacity-40 hover:scale-105 hover:bg-opacity-30 focus:outline-none bg-opacity-20"
    >
      <svg viewBox="0 0 20 20" fill="none" class="w-5 h-5 opacity-70">
        <path
          d="M14.9497 14.9498C12.2161 17.6835 7.78392 17.6835 5.05025 14.9498C2.31658 12.2162 2.31658 7.784 5.05025 5.05033C7.78392 2.31666 12.2161 2.31666 14.9497 5.05033C15.5333 5.63385 15.9922 6.29475 16.3266 7M16.9497 2L17 7H16.3266M12 7L16.3266 7"
          stroke="currentColor"
          stroke-width="1.5"
        />
      </svg>

      <span class="ml-3">Click to transition</span>
    </button>
  </div>
</template>

<script>
import { ref } from "vue";
import { Switch, TransitionRoot } from "@headlessui/vue";
import MyModal from "./components/MyModal.vue";

export default {
  components: { Switch, MyModal, TransitionRoot },

  setup() {
    const enabled = ref(false);
    const isShowing = ref(true);

    // const openModal = ref(false);
    // console.log(openModal.value);
    // const openMyModal = () => {
    //   console.log('open');
    //   openModal.value = true
    // }

    return {
      enabled,
      isShowing,
      resetIsShowing() {
        isShowing.value = false;

        setTimeout(() => {
          isShowing.value = true;
        }, 500);
      },
      // openMyModal
    };
  },
};

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
