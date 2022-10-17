<script setup>
import { storeToRefs } from "pinia";
import { ref } from "vue";
import { useAuthStore } from "../stores/auth.store";
import Spinner from "../utils/Spinner.vue";

const authStore = useAuthStore();
const { state } = storeToRefs(authStore);
const { loginUser } = authStore;

const email = ref("");
const password = ref("");

const onSubmit = () => {
  loginUser({
    email: email.value,
    password: password.value,
  });
};
</script>

<template>
  <div class="container d-flex justify-content-center align-items-center mt-5">
    <div
      class="shadow p-5 d-flex flex-column justify-content-center align-items-center"
    >
      <div class="fs-3 fw-bold mb-4">Login</div>
      <form class="fw-bold" @submit.prevent="onSubmit">
        <div class="mb-3">
          <label for="Email" class="form-label">Email</label>
          <input
            type="email"
            class="form-control"
            id="Email"
            aria-describedby="Email"
            placeholder="Enter Email"
            v-model="email"
            required
          />
        </div>
        <div class="mb-3">
          <label for="Password" class="form-label">Password</label>
          <input
            type="password"
            class="form-control"
            id="Password"
            aria-describedby="Password"
            placeholder="Password"
            v-model="password"
            required
          />
        </div>

        <button type="submit" class="btn btn-info" :disabled="state.loading">
          <span v-if="state.loading">
            <Spinner />
          </span>
          <span v-else> Login </span>
        </button>
      </form>
    </div>
  </div>
</template>
