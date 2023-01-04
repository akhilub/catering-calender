<template>
    <Transition name="fade">
      <div
        v-if="showing"
        @click.self="close"
        class="
          fixed z-50 inset-0 top-0 w-full h-screen flex items-center justify-center bg-semi-75"
      >
        <div class="relative w-full md:max-w-lg bg-white">
          <slot />
        </div>
      </div>
    </Transition>
  </template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  props: {
    showing: {
      required: true,
      type: Boolean,
    },
    redirect: {
      type: Boolean,
    },
  },
  methods: {
    close() {
      this.$emit("close");
    },
  },
});
</script>

  <style scoped>
  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.4s;
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
  </style>