<script setup lang="ts">
import { ref } from "vue";

const inputNameModel = ref("双方向");

const inputNameBind = ref("しんちゃん");
const inputNameOn = ref("ななし");
const onInputName = (event: Event) => {
  const element = event.target as HTMLInputElement;
  inputNameOn.value = element.value;
};

const inputName2Way = ref("双方向");
const onInputName2Way = (event: Event) => {
  const element = event.target as HTMLInputElement;
  inputName2Way.value = element.value;
};

const inputTextarea = ref("テキストエリアへの入力文字。\n改行もくわえてみる。");
const memberType = ref(1);
const memberTypeSelect = ref(1);
const isAggreed = ref(false);
const isAggreed01 = ref(0);
const selectedOS = ref([]);
const selectedOSSelect = ref([]);

const trimedText = ref("");

const htmlStr = ref(`<a href="https://vuejs.org//">Vue.jsのTOPページ</a>`);

const price = ref(1000);

const hello = ref("こんにちは");
</script>

<template>
  <section>
    <input type="text" v-model="inputNameModel" />
    <p>{{ inputNameModel }}</p>
  </section>

  <section>
    <input type="text" v-bind:value="inputNameBind" />
  </section>
  <br />
  <section>
    <input type="text" v-on:input="onInputName" />
    <p>{{ inputNameOn }}</p>
  </section>

  <section>
    <input type="text" v-bind:value="inputName2Way" v-on:input="onInputName2Way" />
    <p>{{ inputName2Way }}</p>
  </section>

  <textarea v-model="inputTextarea"></textarea>
  <br />
  <section>
    <label><input type="radio" name="memberType" value="1" v-model="memberType" />通常会員</label>
    <label><input type="radio" name="memberType" value="2" v-model="memberType" />特別会員</label>
    <label><input type="radio" name="memberType" value="3" v-model="memberType" />優良会員</label>
    <p>選択されたラジオボタン：{{ memberType }}</p>
  </section>
  <section>
    <select v-model="memberTypeSelect">
      <option value="1">通常会員</option>
      <option value="2">特別会員</option>
      <option value="3">優良会員</option>
    </select>
    <p>選択されたリスト：{{ memberTypeSelect }}</p>
  </section>
  <section>
    <label><input type="checkbox" v-model="isAggreed" />同意する</label>
    <p>同意の結果：{{ isAggreed }}</p>
  </section>
  <section>
    <label
      ><input type="checkbox" v-model="isAggreed01" true-value="1" false-value="0" />同意する</label
    >
    <p>同意の結果：{{ isAggreed01 }}</p>
  </section>
  <section>
    <label><input type="checkbox" v-model="selectedOS" value="1" />Windows</label>
    <label><input type="checkbox" v-model="selectedOS" value="2" />macOS</label>
    <label><input type="checkbox" v-model="selectedOS" value="3" />Linux</label>
    <label><input type="checkbox" v-model="selectedOS" value="4" />iOS</label>
    <label><input type="checkbox" v-model="selectedOS" value="5" />Android</label>
    <p>選択されたOS：{{ selectedOS }}</p>
  </section>
  <section>
    <select v-model="selectedOSSelect" multiple>
      <option value="1">macOS</option>
      <option value="2">Windows</option>
      <option value="3">Linux</option>
      <option value="4">iOS</option>
      <option value="5">Android</option>
    </select>
    <p>選択されたOS：{{ selectedOSSelect }}</p>
  </section>

  <section>
    <input type="text" v-model.trim="trimedText" />
    <p>入力文字列：{{ trimedText }}</p>
  </section>

  <section>
    {{ htmlStr }}
  </section>
  <section v-html="htmlStr"></section>

  <section v-pre>
    <p>{{ hello }}</p>
  </section>

  <section>
    <label><input type="number" v-model="price" />円</label>
    <p>金額は{{ price }}円です。</p>
    <p v-once>金額は{{ price }}円です。</p>
  </section>

  <p>v-cloak{{ hello }}</p>
</template>

<style>
[v-cloak] {
  display: none;
}
</style>
