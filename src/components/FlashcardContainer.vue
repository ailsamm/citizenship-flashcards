<script setup lang="ts">
import Button from './Button.vue';
import Flashcard from '@/components/Flashcard.vue';
import { computed, defineProps, onBeforeMount, ref } from 'vue';
import { citizenshipQuestions } from '@/utils/questions';
import { FlashcardData } from '@/utils/global-types';

// ----------------------------------------------------------------
// Props
// ----------------------------------------------------------------
interface Props {
  numberOfQuestions: number;
}

const props = defineProps<Props>();

// ----------------------------------------------------------------
// Emits
// ----------------------------------------------------------------
const emit = defineEmits<{
  (e: 'complete-questions'): void;
}>();

// ----------------------------------------------------------------
// Functionality
// ----------------------------------------------------------------
const orderedQuestions: FlashcardData[] = [...citizenshipQuestions];
const randomizedQuestions = ref<FlashcardData[] | undefined>(undefined);
const currentQuestionIdx = ref(0);
const isAnswerVisible = ref(false);

function selectQuestions(): FlashcardData[] {
  const randomIndices = [];
  while (randomIndices.length < props.numberOfQuestions) {
    const r = Math.floor(Math.random() * 100) + 1; // change to 100
    if (randomIndices.indexOf(r) === -1) randomIndices.push(r);
  }

  return randomIndices.map((i) => {
    return orderedQuestions[i];
  });
}

const progressStatus = computed(() => {
  return `Question ${currentQuestionIdx.value + 1} of ${props.numberOfQuestions}`;
});

function revealAnswer() {
  isAnswerVisible.value = true;
}

function onClickNextQuestion() {
  currentQuestionIdx.value++;
  isAnswerVisible.value = false;
}

function onClickComplete() {
  emit('complete-questions');
}

onBeforeMount(() => {
  randomizedQuestions.value = selectQuestions();
});
</script>

<template>
  <div class="flashcard__outer-container">
    <Flashcard
      v-if="randomizedQuestions"
      :flashcard-data="randomizedQuestions[currentQuestionIdx]"
      :is-answer-visible="isAnswerVisible"
      :progress-status="progressStatus"
    />
    <div class="flashcard__button-container">
      <Button v-if="!isAnswerVisible" :on-click="revealAnswer" label="Reveal answer" />
      <Button
        v-else-if="isAnswerVisible && currentQuestionIdx === numberOfQuestions - 1"
        :on-click="onClickComplete"
        label="Complete"
      />
      <Button v-else-if="isAnswerVisible" :on-click="onClickNextQuestion" label="Next question" />
    </div>
  </div>
</template>

<style lang="postcss">
.flashcard__outer-container {
  display: flex;
  flex-direction: column;
  align-items: center;

  width: 80%;
  height: 550px;

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  & > .flashcard__button-container {
    display: flex;
    justify-content: center;
    align-items: center;

    & > .button-comp {
      &:not(:first-child) {
        margin-left: 1rem;
      }
    }
  }
}
</style>
