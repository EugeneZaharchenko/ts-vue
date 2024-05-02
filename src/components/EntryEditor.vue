<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import {ref, computed} from 'vue';
import type Emoji from '@/types/Emoji'
import Entry from "@/types/Entry";
// import type Ref from 'vue'

const body = ref('AnyVal');
const emoji = ref<Emoji | null>(null);
const charCount = computed<number>(() => body.value.length)
const maxChars = 280;

// events
const emit = defineEmits<{
  (e: '@create', entry: Entry): void;
}>();
// (['@create'])

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
    <textarea :value="body"
    @keyup="handleTextInput" placeholder="Новий журнал for Eugene_Z"></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span> {{ charCount }} / {{maxChars}}</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
