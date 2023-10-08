<script setup lang="ts">
import Button from './Button.vue';
import { ref } from 'vue';

// ----------------------------------------------------------------
// Emits
// ----------------------------------------------------------------
const emit = defineEmits<{
  (e: 'start-questions', num: number): void;
}>();

// ----------------------------------------------------------------
// Functionality
// ----------------------------------------------------------------
const numberOfQuestions = ref(10);

function onClickStart() {
  emit('start-questions', numberOfQuestions.value);
}
</script>

<template>
  <div class="start-screen__container">
    <div class="start-screen__title">
      <h1>Welcome to the Citizenship Test</h1>
      <p>🇺🇸🇺🇸🇺🇸</p>
    </div>

    <label for="input-number">How many questions would you like to test yourself on?</label>
    <div class="input-wrapper">
      <input v-model="numberOfQuestions" id="input-number" type="number" min="1" max="100" />
      <div class="input-controls">
        <button
          aria-label="Decrement number"
          class="cds--number__control-btn down-icon"
          tabindex="-1"
          title="Decrement number"
          type="button"
          :onclick="() => numberOfQuestions--"
        >
          <svg
            focusable="false"
            preserveAspectRatio="xMidYMid meet"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            width="16"
            height="16"
            viewBox="0 0 32 32"
            aria-hidden="true"
            class="down-icon"
          >
            <path d="M8 15H24V17H8z"></path>
          </svg>
        </button>
        <button
          aria-label="Increment number"
          class="cds--number__control-btn up-icon"
          tabindex="-1"
          title="Increment number"
          type="button"
          :onclick="() => numberOfQuestions++"
        >
          <svg
            focusable="false"
            preserveAspectRatio="xMidYMid meet"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            width="16"
            height="16"
            viewBox="0 0 32 32"
            aria-hidden="true"
            class="up-icon"
          >
            <path d="M17 15L17 8 15 8 15 15 8 15 8 17 15 17 15 24 17 24 17 17 24 17 24 15z"></path>
          </svg>
        </button>
        <div class="rule-divider"></div>
      </div>
    </div>
    <Button label="Start" :on-click="onClickStart" />
  </div>
</template>

<style lang="postcss">
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.start-screen__container {
  display: flex;
  flex-direction: column;
  align-items: center;

  position: relative;

  & > label {
    margin-bottom: 1rem;
  }

  & > .input-wrapper {
    width: 200px;
    height: fit-content;

    position: relative;
    display: flex;
    align-items: center;

    position: relative;

    & > input {
      width: 100%;
      height: 100%;
      font-size: 24px;
      text-align: center;
      font-weight: 400;
      line-height: 1.25;
      letter-spacing: 0.16px;
      outline: 2px solid transparent;
      outline-offset: -2px;
      display: inline-flex;
      box-sizing: border-box;
      border: 0;
      border-radius: 0;
      -webkit-appearance: textfield;
      appearance: textfield;
      background-color: #f4f4f4;
      block-size: 2.5rem;
      -webkit-border-after: 0.0625rem solid #8d8d8d;
      border-block-end: 0.0625rem solid #8d8d8d;
      color: #161616;
      font-family: ibm plex sans, system-ui, -apple-system, BlinkMacSystemFont, '.sfnstext-regular',
        sans-serif;
      inline-size: 100%;
      min-inline-size: 9.375rem;
      -webkit-padding-end: 6rem;
      padding-inline-end: 6rem;
      -webkit-padding-start: 1rem;
      padding-inline-start: 1rem;
      transition: background-color 70ms cubic-bezier(0.2, 0, 0.38, 0.9),
        outline 70ms cubic-bezier(0.2, 0, 0.38, 0.9);
    }

    & > .input-controls {
      position: absolute;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: center;
      block-size: 100%;
      inline-size: 5rem;
      inset-block-start: 50%;
      inset-inline-end: 0;
      -webkit-transform: translateY(-50%);
      transform: translateY(-50%);

      & > button {
        box-sizing: border-box;
        padding: 0;
        border: 0;
        margin: 0;
        font-family: inherit;
        font-size: 100%;
        vertical-align: baseline;
        display: inline-block;
        padding: 0;
        border: 0;
        -webkit-appearance: none;
        appearance: none;
        background: 0 0;
        cursor: pointer;
        text-align: start;
        inline-size: 100%;
        position: relative;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        block-size: 100%;
        color: #161616;
        -webkit-border-after: 0.0625rem solid #8d8d8d;
        border-block-end: 0.0625rem solid #8d8d8d;

        &:hover {
          background-color: #e8e8e8;
          color: #161616;
          cursor: pointer;
        }
      }

      & > .rule-divider {
        position: absolute;
        z-index: 6000;
        background-color: #e0e0e0;
        block-size: 1rem;
        inline-size: 0.0625rem;
      }
    }
  }

  & > .start-screen__title {
    font-size: 1.5rem;
    margin-bottom: 2rem;
    text-align: center;

    & > p {
      font-size: 3rem;
    }
  }
}

.button-comp {
  margin-top: 2rem;
}
</style>
