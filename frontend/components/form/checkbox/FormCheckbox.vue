<template>
  <div class="relative flex flex-row items-center justify-start">
    <input
      @keydown="tabToFirstTopic($event)"
      :id="uuid"
      class="connect cursor-pointer mb-0 peer appearance-none w-[1.375rem] h-[1.375rem] border border-light-menu-selection rounded-sm bg-light-button dark:bg-dark-button dark:border-dark-menu-selection focus-brand"
      type="checkbox"
      v-bind="{ ...$attrs, onChange: updateValue }"
      :checked="modelValue"
    />
    <div
      class="pointer-events-none w-[1rem] h-[1rem] hidden absolute left-[0.2rem] bg-light-menu-selection dark:bg-dark-menu-selection peer-checked:block rounded-sm"
    ></div>
    <label
      v-if="label"
      class="ml-2 text-lg cursor-pointer select-none"
      :for="uuid"
    >
      {{ label }}
    </label>
  </div>
</template>

<script setup lang="ts">
import { v4 as uuidv4 } from "uuid";
import useFormInput from "~/composables/useFormSetup";

export interface Props {
  label?: string;
  modelValue?: boolean;
  error?: string;
}

const tabToFirstTopic = (e: KeyboardEvent) => {
  let firstTopic: HTMLElement | null;
  if (window.matchMedia("(min-width: 640px)").matches) {
    firstTopic = document.querySelector(".topic");
  } else {
    firstTopic = document.querySelector(".mobileTopic");
  }

  if (e.shiftKey && e.key == "Tab") {
    e.preventDefault();
    firstTopic?.focus();
    return;
  }
};

const props = withDefaults(defineProps<Props>(), {
  label: "",
  error: "",
});

const emit = defineEmits(["update:modelValue"]);
const { updateValue } = useFormInput(props, emit);
const uuid = uuidv4();
</script>
