<script setup lang="ts">
import { ref, computed, reactive, provide } from "vue";
import OneSection from "./components/OneSection.vue";
import WithModel from "./components/WithModel.vue";
import OneInfo from "./components/OneInfo.vue";
import OneMember from "./components/OneMember.vue";
import OneSection01 from "./components/OneSection01.vue";
import OneMember01 from "./components/OneMember01.vue";
import OneMember02 from "./components/OneMember02.vue";
import BaseSectionVue from "./components/BaseSection.vue";
import type { Member } from "./interfaces";

// 8.3.3
const propsTitle = ref("発生した乱数");
const rand = Math.round(Math.random() * 100);
const propsContent = ref(rand.toString());

// 8.3.4
interface Weather {
  id: number;
  title: string;
  content: string;
}
const weatherListInit = new Map<number, Weather>();
weatherListInit.set(1, { id: 1, title: "今日の天気", content: "今日は一日中、晴れでしょう。" });
weatherListInit.set(2, { id: 2, title: "明日の天気", content: "明日は一日中、雨でしょう。" });
weatherListInit.set(3, { id: 3, title: "明後日の天気", content: "明後日は一日中、雪でしょう。" });
const weatherList = ref(weatherListInit);

// 8.4.1
const memberListInit = new Map<number, Member>();
memberListInit.set(33456, {
  id: 33456,
  name: "田中太郎",
  email: "box@example.com",
  points: 35,
  note: "初回入会特典あり。"
});
memberListInit.set(47783, {
  id: 47783,
  name: "鈴木二郎",
  email: "mue@example.com",
  points: 53
});
const memberList = ref(memberListInit);
const totalPoints = computed((): number => {
  let total = 0;
  for (const member of memberList.value.values()) {
    total += member.points;
  }
  return total;
});

// 8.5.1
const randInit01 = Math.round(Math.random() * 10);
const rand01 = ref(randInit01);
const onCreateNewRand = (): void => {
  rand01.value = Math.round(Math.random() * 10);
};

// 8.5.2
const onIncrementPoint = (id: number): void => {
  const member = memberList.value.get(id);
  if (member != undefined) {
    member.points++;
  }
};

// 8.6.2
provide("memberList", reactive(memberListInit));
</script>

<template>
  <!-- 8.1 -->
  <h1>コンポーネント基礎</h1>
  <section>
    <h2>コンポーネント１個</h2>
    <OneSection />
  </section>
  <section>
    <h2>コンポーネントが複数</h2>
    <OneSection />
    <OneSection />
    <OneSection />
  </section>

  <!-- 8.2 -->
  <h1>コンポーネントの独立性</h1>
  <section>
    <h2>v-modelを含むコンポーネント</h2>
    <WithModel />
    <WithModel />
  </section>

  <!-- 8.3.1 -->
  <h1>Props基礎</h1>
  <section>
    <h2>属性に直接記述</h2>
    <OneInfo title="Propsの利用" content="子コンポーネントにデータを渡すにはPropsを利用する。" />
  </section>

  <!-- 8.3.3 -->
  <h1>Props基礎</h1>
  <section>
    <h2>テンプレート変数を利用</h2>
    <OneInfo v-bind:title="propsTitle" v-bind:content="propsContent" />
  </section>

  <!-- 8.3.4 -->
  <h1>Props基礎</h1>
  <section>
    <h2>ループでコンポーネントを生成</h2>
    <OneInfo
      v-for="[id, weather] in weatherList"
      v-bind:key="id"
      v-bind:title="weather.title"
      v-bind:content="weather.content"
    />
  </section>

  <!-- 8.4.1 -->
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}ポイント</p>
    <OneMember
      v-for="[id, member] in memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-bind:points="member.points"
      v-bind:note="member.note"
    />
  </section>

  <!-- 8.5.1 -->
  <section>
    <p>親コンポーネントで乱数を表示：{{ rand01 }}</p>
    <OneSection01 v-bind:rand="rand01" v-on:create-new-rand="onCreateNewRand" />
  </section>

  <!-- 8.5.2 -->
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}ポイント</p>
    <OneMember01
      v-for="[id, member] in memberList"
      v-bind:key="'OneMember01' + id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-bind:points="member.points"
      v-bind:note="member.note"
      v-on:increment-point="onIncrementPoint"
    />
  </section>

  <!-- 8.5.3 -->
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイントの合計：{{ totalPoints }}ポイント</p>
    <OneMember02
      v-for="[id, member] in memberList"
      v-bind:key="'OneMember02' + id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-model:points="member.points"
      v-bind:note="member.note"
    />
  </section>

  <!-- 8.6.2 -->
  <BaseSectionVue />
</template>

<style>
section {
  border: blue 1px solid;
  margin: 10px;
}
</style>
