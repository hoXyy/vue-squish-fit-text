<template>
  <div ref="fitHost" id="fitHost">
    <div
      :style="{
        maxWidth: `${maxWidth}px`,
      }"
      ref="fittedContent"
      id="fittedContent"
    >
      {{ text }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { PropType, onMounted, watch } from "vue";
import { $ref } from "vue/macros";
type AlignOptions = "left" | "center" | "right";

const fittedContent = $ref<HTMLDivElement>();
const fitHost = $ref<HTMLDivElement>();
const props = defineProps({
  text: {
    type: String,
    required: true,
  },
  maxWidth: {
    type: Number,
    required: true,
    validator(value: number) {
      return value >= 0;
    },
    default: 0,
  },
  align: {
    type: String as PropType<AlignOptions>,
    required: true,
    validator(value: string) {
      return ["left", "center", "right"].includes(value);
    },
    default: "left",
  },
});

onMounted(() => {
  if (fitHost && fittedContent) {
    fit();
    setTextAlign(props.align);
  }
});

watch(props, (newVal) => {
  fit();
  setTextAlign(newVal.align);
});

function setTextAlign(align: AlignOptions) {
  switch (align) {
    case "center":
      fitHost!.style.justifyContent = "center";
      fittedContent!.style.transformOrigin = "center";
      fittedContent!.style.textAlign = "center";
      break;
    case "left":
      fitHost!.style.justifyContent = "";
      fittedContent!.style.transformOrigin = "left";
      fittedContent!.style.textAlign = "left";
      break;
    case "right":
      fitHost!.style.justifyContent = "flex-end";
      fittedContent!.style.transformOrigin = "right";
      fittedContent!.style.textAlign = "right";
  }
}

function fit() {
  fittedContent!.style.transform = "scaleX(1)";

  const scrollWidth = fittedContent!.scrollWidth;
  if (scrollWidth > props.maxWidth) {
    fittedContent!.style.transform = `scaleX(${props.maxWidth / scrollWidth})`;
  } else {
    fittedContent!.style.transform = "scaleX(1)";
  }
}
</script>
