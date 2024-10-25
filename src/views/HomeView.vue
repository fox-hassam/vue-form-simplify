<script setup lang="ts">

import {ref} from "vue";
import Field from "@/components/Field.vue";

type UserData = {
  "firstName": string,
  "lastName": number,
  "email": string,
  "message": string,
  "country": string,
}

const errors = ref({
  firstName: '',
  lastName: '',
  email: '',
  message: '',
  country: '',
});
const formData = ref<UserData>({});

const onSubmitForm = () => {
  validateInputs();

  alert(JSON.stringify(formData.value));
}

const validateInputs = () => {
  errors.value.firstName = formData.value.firstName ? '' : 'First name is required!';
  errors.value.lastName = formData.value.lastName ? '' : 'Last name is required!';
  errors.value.email = formData.value.email ? '' : 'Email is required!';
  errors.value.message = formData.value.message ? '' : 'Message is required!';
  errors.value.country = formData.value.country ? '' : 'Country is required!';
};
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
            <Field
              input-tag="input"
              v-model="formData.firstName"
              id="firstName"
              label="First Name"
              :required="true"
              description="lorem ipsum details..."
              :error-message="errors.firstName"
            />

            <Field
              input-tag="input"
              v-model="formData.lastName"
              id="lastName"
              label="Last Name"
              :required="true"
              description="lorem ipsum details..."
              :error-message="errors.lastName" />
          </div>

          <Field
            input-tag="input"
            v-model="formData.email"
            id="email"
            label="Email"
            :required="true"
            description="lorem ipsum details..."
            :error-message="errors.email" />

          <Field
            input-tag="textarea"
            v-model="formData.message"
            id="message"
            label="Message..."
            :required="true"
            description="lorem ipsum details..."
            :error-message="errors.message" />

          <Field
            input-tag="select"
            id="country"
            label="Chose Country"
            :error-message="errors.country"
            v-slot="slotProps">
            <select
              v-model="formData.country"
              v-bind="slotProps"
              class="mt-2 px-6 py-2 shadow rounded border border-gray:50 bg-white">
              <option value="1">Spain</option>
              <option value="2">Egypt</option>
              <option value="3">Palestine</option>
              <option value="4">China</option>
              <option value="5">Canada</option>
              <option value="6">Mexico</option>
              <option value="7">Uzbekistan</option>
              <option value="8">Others</option>
            </select>
          </Field>

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
