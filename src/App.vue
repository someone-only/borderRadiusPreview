<script setup lang="ts">
import { ref } from "vue";
import { useClipboard } from "@vueuse/core";

const { copy, copied } = useClipboard();

const range = ref([10, 10, 10, 10, 10, 10, 10, 10]);
const color1 = ref();
const color2 = ref();
</script>

<template>
  <div class="flex flex-col items-center min-h-screen">
    <h1 class="text-3xl font-bold text-center mt-4 mb-6 w-[82%]">
      Border Radius Preview
    </h1>
    <div class="relative mb-10">
      <div
        class="relative h-36 w-36 bg-blue-300 shadow-lg z-10"
        :style="{
          backgroundImage:
            'linear-gradient(to bottom right, ' + color1 + ', ' + color2 + ')',
          borderRadius:
            range[0] +
            '%' +
            ' ' +
            range[2] +
            '%' +
            ' ' +
            range[4] +
            '%' +
            ' ' +
            range[6] +
            '%' +
            ' ' +
            '/ ' +
            range[1] +
            '%' +
            ' ' +
            range[3] +
            '%' +
            ' ' +
            range[5] +
            '%' +
            ' ' +
            range[7] +
            '%',
        }"
      ></div>
      <div
        class="h-36 w-36 bg-gray-200 shadow-lg absolute top-4 right-4"
        :style="{
          borderRadius:
            range[0] +
            '%' +
            ' ' +
            range[2] +
            '%' +
            ' ' +
            range[4] +
            '%' +
            ' ' +
            range[6] +
            '%' +
            ' ' +
            '/ ' +
            range[1] +
            '%' +
            ' ' +
            range[3] +
            '%' +
            ' ' +
            range[5] +
            '%' +
            ' ' +
            range[7] +
            '%',
        }"
      ></div>
    </div>
    <div class="grid grid-cols-2 gap-2">
      <input
        v-for="index in 8"
        :key="index"
        class="my-2 h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer dark:bg-gray-700"
        type="range"
        min="0"
        max="100"
        v-model="range[index-1]"
      />
    </div>
    <div class="max-w-[82%] bg-gray-200 p-2 mt-4">
      <p class="text-base" ref="source">
        {{
          range[0] +
          "%" +
          " " +
          range[2] +
          "%" +
          " " +
          range[4] +
          "%" +
          " " +
          range[6] +
          "%" +
          " " +
          "/ " +
          range[1] +
          "%" +
          " " +
          range[3] +
          "%" +
          " " +
          range[5] +
          "%" +
          " " +
          range[7] +
          "%"
        }}
      </p>
    </div>
    <button
      @click="
        copy(
          range[0] +
            '%' +
            ' ' +
            range[2] +
            '%' +
            ' ' +
            range[4] +
            '%' +
            ' ' +
            range[6] +
            '%' +
            ' ' +
            '/ ' +
            range[1] +
            '%' +
            ' ' +
            range[3] +
            '%' +
            ' ' +
            range[5] +
            '%' +
            ' ' +
            range[7] +
            '%'
        )
      "
      type="button"
      class="my-2 px-3 py-2 text-xs font-medium text-center inline-flex items-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
    >
      {{ copied ? "Copied" : "Copy Text To Clipboard" }}
    </button>
    <p class="text-2xl font-bold">Change Color</p>
    <div class="flex items-center gap-4 my-4">
      <color-picker v-model:pureColor="color1" />
      <color-picker v-model:pureColor="color2" />
    </div>
  </div>
</template>

<style scoped></style>
