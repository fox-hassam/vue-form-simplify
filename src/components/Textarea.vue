<script setup lang="ts">
const props = defineProps({
  id: String,
  modelValue: [String, Number],
  rows: Number,
  invalid: Boolean,
  areaDescribedBy: String
});

const emit = defineEmits(["update:modelValue"]);
</script>

<template>
<textarea
  :rows="props.rows"
  placeholder=""
  :class="['mt-2 px-6 py-2 shadow rounded border border-gray:50', {'border-red-500': props.invalid}]"
  @input="(event) => emit('update:modelValue', event.target.value)"></textarea>
</template>
