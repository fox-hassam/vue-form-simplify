<script setup lang="ts">
import {nanoid} from 'nanoid'

const props = defineProps({
  type: String,
  id: String,
  modelValue: [String, Number],
  invalid: Boolean,
  areaDescribedBy: String
});

const emit = defineEmits(["update:modelValuesHandler"]);

</script>

<template>

  <input
    type="text"
    :id="props.id"
    :data-id=nanoid()
    placeholder=""
    :class="['mt-1.5 px-4 py-2 shadow rounded border border-gray:50', {'border-red-500': props.invalid}]"
    :value="props.modelValue"
    @input="$event => emit('update:modelValuesHandler', {id: props.id, value: $event.target.value})"
  />

</template>

<style scoped>

</style>
