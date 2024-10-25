<script setup lang="ts">
const props = defineProps({
  "for": String,
  "required": Boolean
});

</script>

<template>
  <label
    :for="props.for"
    class="">

    <span>
      <slot></slot>
      <span class="text-red-600" v-if="props.required">*</span></span>

    <slot name="description" class="block text-xs font-light text-stone-400" />

  </label>
</template>
