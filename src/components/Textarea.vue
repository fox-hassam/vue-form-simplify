<script setup lang="ts">
const props = defineProps({
  id: String,
  rows: Number
});
</script>

<template>
<textarea
  :rows="props.rows"
  placeholder=""
  class="mt-2 px-6 py-2 shadow rounded"></textarea>
</template>
