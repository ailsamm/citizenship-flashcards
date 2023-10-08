<script setup lang="ts">
import StartScreen from '@/components/StartScreen.vue';
import FlashcardContainer from '@/components/FlashcardContainer.vue';
import { ref } from 'vue';
import EndScreen from '@/components/EndScreen.vue';

// ----------------------------------------------------------------
// Functionality
// ----------------------------------------------------------------
enum PageView {
  START_SCREEN = 'START_SCREEN',
  FLASHCARDS = 'FLASHCARDS',
  END_SCREEN = 'END_SCREEN'
}
const pageView = ref<PageView>(PageView.START_SCREEN);
const numberOfQuestions = ref(1);

function onStartQuestions(num: number) {
  numberOfQuestions.value = num;
  changePageView(PageView.FLASHCARDS);
}

function changePageView(view: PageView) {
  pageView.value = view;
}
</script>

<template>
  <div class="page-wrapper">
    <Transition name="page">
      <StartScreen v-if="pageView === PageView.START_SCREEN" @start-questions="onStartQuestions" />
      <FlashcardContainer
        v-else-if="pageView === PageView.FLASHCARDS"
        :number-of-questions="numberOfQuestions"
        @complete-questions="changePageView(PageView.END_SCREEN)"
      />
      <EndScreen
        v-else-if="pageView === PageView.END_SCREEN"
        @navigate-home="changePageView(PageView.START_SCREEN)"
      />
    </Transition>
  </div>
</template>

<style lang="postcss">
.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s ease;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
  position: absolute;
}

.page-wrapper {
  width: 100%;
  height: 100%;

  background-color: #f2f2f2;

  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
