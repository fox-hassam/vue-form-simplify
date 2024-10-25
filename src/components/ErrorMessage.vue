<script setup lang="ts">

import {nanoid} from "nanoid";
const props = defineProps({
  message: String
});
</script>

<template>
  <span
      :id=nanoid()
      class="block text-xs font-light text-red-800">
    <span v-html="props.message"></span>
  </span>
</template>

<style scoped>

</style>
