<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import {ref, computed, onMounted, inject} from 'vue';
import type Emoji from '@/types/Emoji'
import Entry from "@/types/Entry";
import { userInjectionKey } from "@/injectionKeys";

const body = ref('AnyVal');
const emoji = ref<Emoji | null>(null);
const charCount = computed<number>(() => body.value.length)
const maxChars = 280;
const injectedUser = inject(userInjectionKey)

const textarea = ref<HTMLTextAreaElement | null>(null)
onMounted(() => textarea.value?.focus())

// events
const emit = defineEmits<{
  (e: '@create', entry: Entry): void;
}>();

// methods
const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement
  if (textarea.value.length < maxChars) {
    body.value = textarea.value
  } else {
    body.value = textarea.value = textarea.value.substring(0, maxChars)
  }
}

const handleSubmit = () => {
  emit('@create', 
  { userId: 1,
    body: body.value,
    emoji: emoji.value,
    createdAt: new Date(),
    id: Math.random()
  })
}
body.value = ''
emoji.value = null
</script>

<template>
  <form class="entry-form" @submit.prevent="handleSubmit">
    <textarea
      ref="textArea"
      v-model="body"
      @keyup="handleTextInput"
      :placeholder="`New entry for Mr. ${
        injectedUser?.username || 'anonymous'
      }`"
    ></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>{{ charCount }} / {{ maxChars }}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
