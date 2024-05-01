<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import {ref, computed} from 'vue';
import type Emoji from '@/types/Emoji'
// import type Ref from 'vue'

const text = ref('AnyVal');
const emoji = ref<Emoji | null>(null);
// emoji.value = 'asdf'
const charCount = computed<number>(() => text.value.length)
const maxChars = 280;

// events
defineEmits<{
  (e: '@create', entry: {text: string, emoji: Emoji | null}): void;
}>();
// (['@create'])

// methods
const handleTextInput = (e: Event) => {
  const textarea = e.target as HTMLTextAreaElement
  if (textarea.value.length < maxChars) {
    text.value = textarea.value
  } else {
    text.value = textarea.value = textarea.value.substring(0, maxChars)
  }
}
</script>

<template>
  <form class="entry-form" @submit.prevent="$emit('@create', {text, emoji})">
    <textarea :value="text"
    @keyup="handleTextInput" placeholder="Новий журнал for Eugene_Z"></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span> {{ charCount }} / {{maxChars}}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
