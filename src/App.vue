<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { reactive } from 'vue';
import type User from '@/types/User'
import Emoji from "./types/Emoji";

const user: User = reactive(
  {
    id: 1,
    username: 'Eugene',
    settings: []
  }
)
console.log(user.id);
const handleCreateEntry = (entry: {text: string, emoji: Emoji | null}) => {
  console.log(entry)
}
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry"/>
    <ul>
      <li>
        <EntryCard />
      </li>
    </ul>
  </main>
</template>
