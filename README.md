# [vue-squish-fit-text](https://www.npmjs.com/package/vue-squish-fit-text)

## Introduction
_A port of [sc-fitted-text](https://github.com/SupportClass/sc-fitted-text) to a Vue 3 Component._

### Motivation
Broadcast graphics often need to ensure that text will fit within a given space. There are existing libraries out there that can reduce the font size of an element to fit a given space, but this behavior isn't always what is wanted. Sometimes, the design calls for horizontally squishing (scaling) the text, rather than reducing the font size. This element enables that.

## Installation

```
npm install vue-squish-fit-text
```
and then register it either globally:
```ts
import { createApp } from "vue";
import "./style.css";
import App from "./App.vue";
import VueSquishFitText from "vue-squish-fit-text";

createApp(App).component("squish-fit-text", VueSquishFitText).mount("#app");
```
or locally:
```vue
<script setup lang="ts">
import VueSquishFitText from "vue-squish-fit-text";
...
</script>

<template>
   <vue-squish-fit-text text="This text will be fitted." :maxWidth="250" align="left" />
</template>
```

## Properties
| Property name   | Value type accepted   | Default |
| :-------------: | :------------------:  | :------: |
| text | `string` | None |
| maxWidth | `number` | 0 |
| align | `left`, `center` or `right` | `left` |