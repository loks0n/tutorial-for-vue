<script setup>
import { user } from "../stores/user";
import { ideas } from "../stores/ideas";
import { onMounted, ref } from "vue";

const title = ref("");
const description = ref("");

function addIdea() {
  ideas.add({
    userId: user.current.$id,
    title: title.value,
    description: description.value,
  });
  title.value = "";
  description.value = "";
}

onMounted(() => {
  ideas.init();
});
</script>

<template>
  <section v-if="user.current" class="card">
    <h2 class="heading-level-2">Submit Idea</h2>

    <form class="u-flex-vertical u-margin-block-start-16 u-gap-8">
      <input
        class="input-text"
        type="text"
        placeholder="Title"
        v-model="title"
      />
      <textarea
        class="input-text"
        placeholder="Description"
        v-model="description"
      ></textarea>
      <button class="button" type="button" @click="addIdea()">Submit</button>
    </form>
  </section>
  <section v-else class="card"><p>Please login to submit an idea.</p></section>

  <section v-if="ideas.current" class="card">
    <h2 class="heading-level-2">Latest Ideas</h2>
    <ul class="boxes-wrapper u-margin-block-start-16">
      <li v-for="idea in ideas.current" class="box u-flex-vertical u-gap-8">
        <strong class="u-bold">{{ idea.title }}</strong>
        <p>{{ idea.description }}</p>
        <button
          v-if="user.current && idea.userId === user.current.$id"
          class="button is-secondary"
          type="button"
          @click="ideas.remove(idea.$id)"
        >
          Remove
        </button>
      </li>
    </ul>
  </section>
</template>
