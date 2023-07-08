<script setup lang="ts">
import { ref, computed } from "vue";

const number = ref(80);
const showOrNot = computed((): boolean => {
  let showOrNot = false;
  const rand = Math.round(Math.random() * 100);
  if (rand >= 50) {
    showOrNot = true;
  }
  return showOrNot;
});

const randomNumber = computed((): number => {
  return Math.round(Math.random() * 100);
});

const cocktailListInit: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cocktailList = ref(cocktailListInit);

const cocktailListInit01: { [key: number]: string } = {
  2345: "ホワイトレディ",
  4412: "ブルーハワイ",
  6792: "ニューヨーク"
};
const cocktailList01 = ref(cocktailListInit01);

const cocktailListInit02 = new Map<number, string>();
cocktailListInit02.set(2345, "ホワイトレディ");
cocktailListInit02.set(4412, "ブルーハワイ");
cocktailListInit02.set(6792, "ニューヨーク");
const cocktailList02 = ref(cocktailListInit02);

const whiteLadyInit: {
  id: number;
  name: string;
  price: number;
  receipe: string;
} = {
  id: 2345,
  name: "ホワイトレディ",
  price: 1200,
  receipe: "ジン30ml+コアントロー15ml+レモン果汁15ml"
};
const whiteLady = ref(whiteLadyInit);

interface Cocktail {
  id: number;
  name: string;
  price: number;
}
const cocktailDataListInit: Cocktail[] = [
  {
    id: 2345,
    name: "ホワイトレディ",
    price: 1200
  },
  {
    id: 4412,
    name: "ブルーハワイ",
    price: 1500
  },
  {
    id: 6792,
    name: "ニューヨーク",
    price: 1100
  },
  {
    id: 8429,
    name: "マティーニ",
    price: 1500
  }
];
const cocktailDataList = ref(cocktailDataListInit);

const cocktailDataListInit01 = new Map<number, Cocktail>();
cocktailDataListInit01.set(2345, {
  id: 2345,
  name: "ホワイトレディ",
  price: 1200
});
cocktailDataListInit01.set(4412, {
  id: 4412,
  name: "ブルーハワイ",
  price: 1500
});
cocktailDataListInit01.set(6792, {
  id: 6792,
  name: "ニューヨーク",
  price: 1100
});
cocktailDataListInit01.set(8429, {
  id: 8429,
  name: "マティーニ",
  price: 1500
});
const cocktailDataList01 = ref(cocktailDataListInit01);

const cocktail1500 = computed((): Cocktail[] => {
  const newList = cocktailDataList.value.filter((cocktailItem: Cocktail): boolean => {
    return cocktailItem.price == 1500;
  });
  return newList;
});

const cocktailListInit03: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cocktailList03 = ref(cocktailListInit03);
const changeCocktailList = (): void => {
  cocktailList03.value = ["バラライカ", "XYZ", "マンハッタン"];
};
const addCocktailList = (): void => {
  cocktailList03.value.push("ブルームーン");
};
const deleteFromCocktailList = (): void => {
  cocktailList03.value.pop();
};

const changeCocktailList01 = (): void => {
  cocktailList02.value.clear();
  cocktailList02.value.set(3416, "バラライカ");
  cocktailList02.value.set(5517, "XYZ");
  cocktailList02.value.set(7415, "マンハッタン");
};
const addCocktailList01 = (): void => {
  cocktailList02.value.set(8894, "ブルームーン");
};
const deleteFromCocktailList01 = (): void => {
  cocktailList02.value.delete(5517);
};

const changeWhiteLadyPrice = (): void => {
  whiteLady.value.price = 1500;
};

const cocktail150001 = computed((): Map<number, Cocktail> => {
  const newList = new Map<number, Cocktail>();
  cocktailDataList01.value.forEach((value: Cocktail, key: number) => {
    if (value.price == 1500) {
      newList.set(key, value);
    }
  });
  return newList;
});
const changeWhiteLadyPriceInList = (): void => {
  const whiteLady = cocktailDataList01.value.get(2345) as Cocktail;
  whiteLady.price = 1500;
};
</script>

<template>
  <p v-if="number >= 50">条件に合致したので表示①</p>
  <p v-if="Math.round(Math.random() * 100) >= 50">条件に合致したので表示②</p>
  <p v-if="showOrNot">条件に合致したので表示③</p>

  <p>
    点数は{{ randomNumber }}で
    <span v-if="randomNumber >= 80">優です。</span>
    <span v-else-if="randomNumber >= 70">良です。</span>
    <span v-else-if="randomNumber >= 60">可です。</span>
    <span v-else>不可です。</span>
  </p>

  <p>
    点数は{{ randomNumber }}点<template v-if="randomNumber >= 80"
      >で良です。<span style="color: red">素晴らしい！</span></template
    >
  </p>

  <section>
    v-ifを使用
    <p v-if="showOrNot">条件に合致したので表示</p>
  </section>
  <section>
    v-showを使用
    <p v-show="showOrNot">条件に合致したので表示</p>
  </section>

  <ul>
    <li v-for="cocktailName in cocktailList" v-bind:key="cocktailName">{{ cocktailName }}</li>
  </ul>
  <ul>
    <li v-for="(cocktailName, index) in cocktailList" v-bind:key="cocktailName">
      {{ cocktailName }}（インデックス{{ index }}）
    </li>
  </ul>

  <ul>
    <li v-for="(cocktailName, id) in cocktailList01" v-bind:key="'cocktailList' + id">
      IDが{{ id }}のカクテルは{{ cocktailName }}
    </li>
  </ul>
  <ul>
    <li v-for="(cocktailName, id, index) in cocktailList01" v-bind:key="'cocktailListWithIdx' + id">
      {{ index + 1 }}：IDが{{ id }}のカクテルは{{ cocktailName }}
    </li>
  </ul>

  <ul>
    <li v-for="[id, cocktailName] in cocktailList02" v-bind:key="'cocktailListWithMap' + id">
      IDが{{ id }}のカクテルは{{ cocktailName }}
    </li>
  </ul>

  <dl>
    <template v-for="(value, key) in whiteLady" v-bind:key="key">
      <dt>{{ key }}</dt>
      <dd>{{ value }}</dd>
    </template>
  </dl>

  <ul>
    <li v-for="cocktailItem in cocktailDataList" v-bind:key="'cocktailDataList' + cocktailItem.id">
      {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
    </li>
  </ul>

  <ul>
    <li
      v-for="[id, cocktailItem] in cocktailDataList01"
      v-bind:key="'cocktailDataListWithMap' + id"
    >
      {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
    </li>
  </ul>

  <ul>
    <li v-for="r in 5" v-bind:key="r">半径{{ r }}の円の円周：{{ 2 * r * 3.14 }}</li>
  </ul>

  <select>
    <option v-for="year in 5" v-bind:key="year" v-bind:value="year + 1965">
      {{ year + 1965 }}年
    </option>
  </select>

  <section>
    値段が1500円のカクテル
    <ul>
      <li v-for="cocktailItem in cocktail1500" v-bind:key="'cocktail1500' + cocktailItem.id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </section>

  <ul>
    <li
      v-for="(cocktailName, index) in cocktailList03"
      v-bind:key="'cocktailList03' + cocktailName"
    >
      {{ cocktailName }}（インデックス{{ index }}）
    </li>
  </ul>
  <p>CocktailListを<button v-on:click="changeCocktailList">変更</button></p>
  <p>CocktailListの末尾に「ブルームーン」を<button v-on:click="addCocktailList">追加</button></p>
  <p>CocktailListから末尾の要素を<button v-on:click="deleteFromCocktailList">削除</button></p>

  <ul>
    <li v-for="[id, cocktailName] in cocktailList02" v-bind:key="'cocktailListWithMap01' + id">
      IDが{{ id }}のカクテルは{{ cocktailName }}
    </li>
  </ul>
  <p>CocktailListを<button v-on:click="changeCocktailList01">変更</button></p>
  <p>CocktailListの末尾に「ブルームーン」を<button v-on:click="addCocktailList01">追加</button></p>
  <p>CocktailListから5517のXYZを<button v-on:click="deleteFromCocktailList01">削除</button></p>

  <dl>
    <template v-for="(value, key) in whiteLady" v-bind:key="key">
      <dt>{{ key }}</dt>
      <dd>{{ value }}</dd>
    </template>
  </dl>
  <p>価格を1500円に<button v-on:click="changeWhiteLadyPrice">変更</button></p>

  <section>
    全てのカクテルリスト
    <ul>
      <li
        v-for="[id, cocktailItem] in cocktailDataList01"
        v-bind:key="'cocktailDataListWithMap' + id"
      >
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </section>
  <section>
    値段が1500円のカクテルリスト
    <ul>
      <li v-for="[id, cocktailItem] in cocktail150001" v-bind:key="'cocktail150001' + id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </section>
  <p>
    CocktaiDataList内のホワイトレディの価格を1500円に
    <button v-on:click="changeWhiteLadyPriceInList">変更</button>
  </p>
</template>
