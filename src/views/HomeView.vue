<script setup lang="ts">

import {ref} from "vue";
import Label from "@/components/Label.vue";

type UserData = {
  "firstName": string,
  "lastName": number,
  "email": string,
  "message": string
}

const errors = ref();
const formData = ref<UserData>({});

const onSubmitForm = () => {
  errors.value = {
    firstName: 'First name is required!',
    lastName: 'Last name is required!',
    email: 'Email name is required!',
  };
  console.log(formData.value);
  console.log(errors.value);
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
              <input
                type="text"
                id="firstName"
                placeholder=""
                class="mt-2 px-4 py-2 shadow rounded"
                v-model:="formData.firstName"
              />
              <span class="block text-xs font-light text-red-800">First name is required!</span>
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
              <input
                type="text"
                placeholder=""
                class="mt-2 px-4 py-2 shadow rounded"
                v-model:="formData.lastName"/>
              <span class="block text-xs font-light text-red-800">Last name is required!</span>
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
            <input
              type="email"
              id="email"
              placeholder=""
              class="mt-2 px-4 py-2 shadow rounded"
              v-model:="formData.email"/>
            <span class="block text-xs font-light text-red-800">Email name is required!</span>
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
            <textarea
              rows="5"
              placeholder=""
              class="mt-2 px-6 py-2 shadow rounded"
              v-model:="formData.message"></textarea>
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
