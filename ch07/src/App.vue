<script setup lang="ts">
import { ref, computed, watchEffect, watch } from "vue";

interface Cocktail {
  id: number;
  name: string;
  price: number;
}

// 7.1.1
const cocktailDataListInit = new Map<number, Cocktail>();
cocktailDataListInit.set(1, { id: 1, name: "ホワイトレディ", price: 1200 });
cocktailDataListInit.set(2, { id: 2, name: "ブルーハワイ", price: 1500 });
cocktailDataListInit.set(3, { id: 3, name: "ニューヨーク", price: 1100 });
cocktailDataListInit.set(4, { id: 4, name: "マティーニ", price: 1500 });

const cocktailNo = ref(1);
const priceMsg = computed((): string => {
  const cocktail = cocktailDataListInit.get(cocktailNo.value);
  let msg = "該当カクテルはありません";
  if (cocktail != undefined) {
    msg = `該当カクテルは${cocktail.name}で、価格は${cocktail.price}円です`;
  }
  return msg;
});
setInterval((): void => {
  cocktailNo.value = Math.round(Math.random() * 3) + 1;
}, 1000);

// 7.1.2
const priceMsg01 = ref("");
watchEffect((): void => {
  priceMsg01.value = getCocktailInfo(cocktailNo.value);
});
function getCocktailInfo(cocktailNo: number): string {
  const cocktailDataListInit = new Map<number, Cocktail>();
  cocktailDataListInit.set(1, { id: 1, name: "ホワイトレディ", price: 1200 });
  cocktailDataListInit.set(2, { id: 2, name: "ブルーハワイ", price: 1500 });
  cocktailDataListInit.set(3, { id: 3, name: "ニューヨーク", price: 1100 });
  cocktailDataListInit.set(4, { id: 4, name: "マティーニ", price: 1500 });

  const cocktail = cocktailDataListInit.get(cocktailNo);
  let msg = "該当カクテルはありません";
  if (cocktail != undefined) {
    msg = `該当カクテルは${cocktail.name}で、価格は${cocktail.price}円です`;
  }
  return msg;
}

// 7.1.3
const priceMsg02 = ref("");
watch(
  cocktailNo,
  (): void => {
    priceMsg02.value = getCocktailInfo(cocktailNo.value);
  },
  { immediate: true }
);

// 7.1.5
const priceMsg03 = ref("");
watch(cocktailNo, (newVal: number, oldVal: number): void => {
  let msg = "前のカクテル：";
  msg += getCocktailInfo(oldVal);
  msg += "<br />";
  msg += "現在のカクテル：";
  msg += getCocktailInfo(newVal);
  priceMsg03.value = msg;
});
</script>

<template>
  <!-- 7.1.1 -->
  <p>現在のカクテル番号：{{ cocktailNo }}</p>
  <p>{{ priceMsg }}</p>

  <!-- 7.1.2 -->
  <p>現在のカクテル番号：{{ cocktailNo }}</p>
  <p>{{ priceMsg01 }}</p>

  <!-- 7.1.3 -->
  <p>現在のカクテル番号：{{ cocktailNo }}</p>
  <p>{{ priceMsg02 }}</p>

  <!-- 7.1.5 -->
  <p>現在のカクテル番号：{{ cocktailNo }}</p>
  <p v-html="priceMsg03"></p>
</template>
