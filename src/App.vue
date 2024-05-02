<script setup lang="ts">
import TheHeader from "@/components/TheHeader.vue";
import EntryEditor from "./components/EntryEditor.vue";
import EntryCard from "@/components/EntryCard.vue";
import { reactive, provide } from 'vue';
import type User from '@/types/User'
import Entry from "./types/Entry";
import { userInjectionKey } from "./injectionKeys";

const entries: Entry[] = reactive([])

const user: User = reactive(
  {
    id: 1,
    username: 'Eugene',
    settings: []
  }
)
provide(userInjectionKey, user);

const handleCreateEntry = (entry: Entry) => {
  entries.unshift(entry)
}
</script>

<template>
  <main class="container m-auto p-10">
    <TheHeader />
    <EntryEditor @@create="handleCreateEntry"/>
    <ul>
      <li v-for="entryItem in entries" :key="entryItem.id">
        <EntryCard :entry="entryItem" :random-prop="entryItem.body" />
      </li>
    </ul>
  </main>
</template>
