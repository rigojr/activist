<template>
  <a
    class="btn-base-class rounded-md xl:rounded-lg"
    :class="btnDynamicClass"
    :href="linkTo"
    :aria-label="$t(ariaLabel)"
  >
    <BtnIconsLabel
      :label="label"
      :leftIcon="leftIcon"
      :rightIcon="rightIcon"
      :iconSize="iconSize"
    />
  </a>
</template>

<script setup lang="ts">
import type { BtnRoute } from "~/types/btn-props";
import { getBtnDynamicClass } from "~/utils/btnUtils";

const props = defineProps<BtnRoute>();

const btnDynamicClass = getBtnDynamicClass(props.cta, props.fontSize);
</script>
