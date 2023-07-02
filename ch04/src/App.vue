<script setup lang="ts">
import { ref } from "vue";

const url = ref("https://vuejs.org/");

const isSendButtonDisabled = ref(true);

const widthOrHeight = ref("height");
const widthOrHeightValue = ref(100);

const imageAttributes = ref({
  src: "/images/logo.svg",
  alt: "Vueのロゴ",
  width: 75,
  height: 75
});
</script>

<template>
  <p><a v-bind:href="url" target="_blank">Vue.jsのサイト</a></p>
  <p><a :href="url" target="_blank">Vue.jsのサイト（省略形）</a></p>
  <p><a v-bind:href="url + 'guide/introduction.html'">vue.jsガイドページ</a></p>
  <p><button type="button" v-bind:disabled="isSendButtonDisabled">送信</button></p>
  <p><img alt="VueLogo" src="./assets/logo.svg" v-bind:[widthOrHeight]="widthOrHeightValue" /></p>
  <p><img v-bind="imageAttributes"></p>
  <p><img v-bind="imageAttributes" title="ロゴです！"></p>
  <p><img v-bind="imageAttributes" alt="ロゴです"></p>
</template>
