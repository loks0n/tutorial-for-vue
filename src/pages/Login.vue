<script setup>
import { user } from "../stores/user";
import { ref } from "vue";

const email = ref("");
const password = ref("");
</script>

<template>
  <section class="card">
    <h1 class="heading-level-1">Login or register</h1>
    <form
      class="form u-margin-block-start-16 u-gap-16 u-width-full-line u-max-width-500"
    >
      <input
        class="input-text"
        type="email"
        placeholder="Email"
        v-model="email"
      />
      <input
        class="input-password"
        type="password"
        placeholder="Password"
        v-model="password"
      />
      <div class="u-flex u-gap-8">
        <button
          class="button"
          type="button"
          @click="user.login(email, password)"
        >
          Login
        </button>
        <button
          class="button"
          type="button"
          @click="user.register(email, password)"
        >
          Register
        </button>
      </div>
    </form>
  </section>
</template>
