<script lang="ts" setup>
import EmojiField from "@/components/EmojiField.vue";
import ArrowCircleRight from "@/assets/icons/arrow-circle-right.svg";
import {ref} from 'vue';
import type Emoji from '@types/Emoji'
// import type Ref from 'vue'

const text = ref('AnyVal');
const emoji = ref<Emoji | null>(null);
// emoji.value = 'asdf'
</script>

<template>
  <form class="entry-form" @submit.prevent>
    <textarea v-model="text" placeholder="Новий журнал for Eugene_Z"></textarea>
    <EmojiField v-model="emoji" />
    <div class="entry-form-footer">
      <span>0 / 280</span>
      <button>Remember <ArrowCircleRight width="20" /></button>
    </div>
  </form>
</template>
