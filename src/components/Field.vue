<script setup lang="ts">

import Label from "@/components/Label.vue";
import ErrorMessage from "@/components/ErrorMessage.vue";
import Input from "@/components/Input.vue";
import Textarea from "@/components/Textarea.vue";
import {nanoid} from "nanoid";

const props = defineProps({
  "inputTag": String,
  "id": {
    type: String,
    default: () => `input-${nanoid()}`
  },
  "label": String,
  "required": Boolean,
  "description": String,
  "errorMessage": String,
  "modelValue": String // receiving v-model value from HomeView.vue
});

const emit = defineEmits(["update:modelValue"]);
const updateValue = (value: string) => {
  emit("update:modelValue", value); // emit value changes to Home.vue
};

</script>

<template>
  <div class="flex flex-col mb-4">
    <Label
      v-if="props.label"
      :for="props.id"
      :required="props.required">
      {{ props.label }}
      <template v-slot:description>
        <span class="block text-xs font-light text-stone-400" v-if="props.description">{{ props.description }}</span>
      </template>
    </Label>
    <slot
      v-if="!['input', 'textarea'].includes(props.inputTag)"
      v-bind="props"
    />
    <Input
      v-if="props.inputTag === 'input'"
      type="text"
      :id="props.id"
      :model-value="modelValue"
      :invalid="!!props.errorMessage"
      @update:modelValue="updateValue" />
    <Textarea
      v-if="props.inputTag === 'textarea'"
      :id="props.id"
      :model-value="modelValue"
      :rows="3"
      :invalid="!!props.errorMessage"
      @update:modelValue="updateValue" />

    <ErrorMessage v-if="props.errorMessage" :message="props.errorMessage"/>
  </div>
</template>

<style scoped>

</style>
