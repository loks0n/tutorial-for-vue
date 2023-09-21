<script setup>
import { onMounted } from "vue";
import Home from "./pages/Home.vue";
import Login from "./pages/Login.vue";
import { user } from "./stores/user.js";

const isLoginPage = window.location.pathname === "/login";

onMounted(() => {
  user.init();
});
</script>

<template>
  <div class="u-padding-16 u-max-width-600 u-full-width" style="margin: 0 auto">
    <nav
      class="u-flex u-main-space-between u-cross-center u-gap-16 u-padding-16"
    >
      <a class="heading-level-6" href="/">Idea Tracker</a>
      <div class="u-flex u-gap-16 u-cross-center">
        <template v-if="user.current">
          <span>{{ user.current.email }}</span>
          <button class="button" type="button" @click="user.logout()">
            Logout
          </button>
        </template>
        <a v-else class="button" href="/login">Login</a>
      </div>
    </nav>
    <main class="u-flex-vertical u-gap-16">
      <Login v-if="isLoginPage" />
      <Home v-else />
    </main>
  </div>
</template>
