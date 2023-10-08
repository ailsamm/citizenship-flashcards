<script setup lang="ts">
import { computed, defineProps, ref, watch } from 'vue';
import { FlashcardData } from '@/utils/global-types';

// ----------------------------------------------------------------
// Props
// ----------------------------------------------------------------
interface Props {
  flashcardData: FlashcardData;
  isAnswerVisible: boolean;
  progressStatus: string;
}

const props = defineProps<Props>();

// ----------------------------------------------------------------
// Functionality
// ----------------------------------------------------------------
const updateKey = ref(0);

watch(
  () => props.flashcardData,
  () => {
    updateKey.value++;
  }
);

const answers = computed(() => {
  return props.flashcardData.answer.split('*').filter((answer: string) => answer);
});
</script>

<template>
  <div class="flashcard__inner-container">
    <header class="flashcard__header">{{ props.progressStatus }}</header>
    <Transition>
      <div
        :class="['flashcard__content-container', { 'is-answer-visible': props.isAnswerVisible }]"
        :key="updateKey"
      >
        <div class="flashcard__question">{{ props.flashcardData.question }}</div>
        <template v-if="props.isAnswerVisible">
          <div class="flashcard__horizontal-line" />
          <ul
            :class="[
              'flashcard__answer',
              { 'has-one-answer': answers.length === 1, 'excessive-answers': answers.length >= 6 }
            ]"
          >
            <li v-for="(answer, i) in answers" :key="i">{{ answer.trim() }}</li>
          </ul>
        </template>
      </div>
    </Transition>
  </div>
</template>

<style lang="postcss">
:root {
  --highlight-color: #5482c8;
}

/*.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
  transform: translateY(-20px);
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
  position: absolute;
}*/

.flashcard__inner-container {
  width: 100%;
  height: 100%;

  box-shadow: 0 4px 8px rgba(28, 34, 36, 0.16);

  & > .flashcard__header {
    background: rgb(69, 116, 189);
    background: linear-gradient(
      90deg,
      rgba(69, 116, 189, 1) 0%,
      rgba(84, 130, 200, 0.7553615196078431) 42%,
      rgba(84, 130, 200, 0.14471726190476186) 100%
    );
    color: white;

    width: calc(100% + 0.5px);

    border: none;
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;

    display: flex;
    align-items: center;

    font-weight: 600;
    font-size: 1.125rem;
    height: 2.5rem;
    padding: 4px 8px;
  }

  & > .flashcard__content-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    background-color: white;

    border: 1px solid #c1c1c1;
    border-top: none;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;

    height: calc(100% - 2.5rem);

    padding: 1.5rem 3rem;

    & > .flashcard__question {
      font-size: 32px;
      text-align: center;
    }

    & > .flashcard__answer {
      font-size: 24px;
      padding-left: 0;

      &.has-one-answer > li {
        list-style: none;
      }

      &.excessive-answers {
        column-count: 2;
        column-gap: 4rem;
      }
    }

    & > .flashcard__horizontal-line {
      width: 60%;
      height: 4px;
      border-radius: 4px;
      background-color: var(--highlight-color);
    }

    &.is-answer-visible {
      & > .flashcard__answer {
        margin-top: 4rem;
      }
      & > .flashcard__question {
        margin-bottom: 2rem;
      }
    }
  }
}
</style>
