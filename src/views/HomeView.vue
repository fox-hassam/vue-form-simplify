<script setup lang="ts">

import {ref} from "vue";
import Label from "@/components/Label.vue";
import Input from "@/components/Input.vue";
import Textarea from "@/components/Textarea.vue";
import ErrorMessage from "@/components/ErrorMessage.vue";

type UserData = {
  "firstName": string,
  "lastName": number,
  "email": string,
  "message": string
}

const errors = ref({
  firstName: '',
  lastName: '',
  email: '',
  message: ''
});
const formData = ref<UserData>({});

const onSubmitForm = () => {
  const validated = validateInputs();
  console.log(validated)

  console.log(formData.value);
}

const validateInputs = () => {
  if (!formData.value.firstName || formData.value.firstName === '') {
    errors.value.firstName = 'First name is required!';
  }
  if (!formData.value.lastName || formData.value.lastName === '') {
    errors.value.lastName = 'Last name is required!';
  }
  if (!formData.value.email || formData.value.email === '') {
    errors.value.email = 'Email name is required!';
  }
  if (!formData.value.message || formData.value.message === '') {
    errors.value.message = 'Message is required!';
  }

  return errors.value;
}

const modelValuesHandler = (attr) => {
  formData.value = {
    ...formData.value,
    [attr.id]: attr.value
  }

  errors.value = {
    ...errors.value,
    [attr.id]: ''
  }

  console.log(formData.value)
}
</script>

<template>
  <main>
    <!-- <TheWelcome />-->
    <div class="flex items-center justify-center bg-stone-100 p-4 w-full">
      <div class="p-6 rounded shadow-sm bg-stone-50 max-w-lg">
        <div class="mb-6 p-6 bg-white">
          <h1 class="font-bold text-2xl text-stone-700">Details</h1>
        </div>
        <form autocomplete="off" @submit.prevent="onSubmitForm">
          <div class="grid grid-cols-2 gap-2.5">
            <div class="flex flex-col mb-4">
              <Label
                for="firstName"
                :required="true">
                First Name
                <template v-slot:description>
                  <span class="block text-xs font-light text-stone-400">lorem ipsum details...</span>
                </template>
              </Label>
              <Input
                type="text"
                id="firstName"
                model-value=""
                :invalid="!!errors.firstName"
                @update:model-values-handler="modelValuesHandler" />
              <ErrorMessage v-if="errors.firstName" message="First name is required!" />
            </div>
            <div class="flex flex-col mb-4">
              <Label
                for="firstName"
                :required="true">
                Last Name
                <template v-slot:description>
                  <span class="block text-xs font-light text-stone-400">lorem ipsum details</span>
                </template>
              </Label>
              <Input
                type="text"
                id="lastName"
                model-value=""
                :invalid="!!errors.lastName"
                @update:model-values-handler="modelValuesHandler"
              />
              <ErrorMessage v-if="errors.lastName" message="Last name is required!" />
            </div>
          </div>
          <div class="flex flex-col mb-4">
            <Label
              for="email"
              :required="true">
              Email
              <template v-slot:description>
                <span class="block text-xs font-light text-stone-400">lorem ipsum details</span>
              </template>
            </Label>
            <Input type="text"
                   id="email"
                   :invalid="!!errors.email"
                   @update:model-values-handler="modelValuesHandler"
            />
            <ErrorMessage v-if="errors.email" message="Email name is required!" />
          </div>
          <div class="flex flex-col mb-4">
            <Label
              for="message"
              :required="true">
              Message
              <template v-slot:description>
                <span class="block text-xs font-light text-stone-400">lorem ipsum details</span>
              </template>
            </Label>
            <Textarea
              id="message"
              :rows="3"
              :invalid="!!errors.message"
              @update:model-values-handler="modelValuesHandler" />
            <ErrorMessage v-if="errors.message" message="Required field" />
          </div>
          <div class="mt-6 flex gap-6">
            <button type="submit" class="rounded-full bg-orange-400 py-2 px-10 font-bold text-white shadow hover:bg-orange-500">
              Button
            </button>
          </div>
        </form>
      </div>
    </div>
  </main>
</template>
