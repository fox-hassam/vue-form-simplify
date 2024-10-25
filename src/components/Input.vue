<script setup lang="ts">
import {nanoid} from 'nanoid'

const props = defineProps({
  type: String,
  id: String
});

</script>

<template>

  <input
    type="text"
    :id="props.id"
    :data-id=nanoid()
    placeholder=""
    class="mt-1.5 px-4 py-2 shadow rounded"
  />

</template>

<style scoped>

</style>
