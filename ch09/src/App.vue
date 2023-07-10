<script setup lang="ts">
import { ref } from "vue";
import OneSection from "./components/OneSection.vue";
import OneSection01 from "./components/OneSection01.vue";
import NameInput from "./components/NameInput.vue";
import MemberTypeRadio from "./components/MemberTypeRadio.vue";
import MemberTypeSelect from "./components/MemberTypeSelect.vue";

const kazu = ref("佐藤一郎");
const taro = ref("田中太郎");
const taroProblemsInit: string[] = ["電話が通じません。", "留守です。"];
const taroProblems = ref(taroProblemsInit);
const jiro = ref("鈴木二郎");

// 9.4.1
const currentComp = ref(NameInput);
const currentCompName = ref("NameInput");
const compList = [NameInput, MemberTypeRadio, MemberTypeSelect];
const compNameList: string[] = ["NameInput", "MemberTypeRadio", "MemberTypeSelect"];
let currentCompIndex = 0;
const switchComp = (): void => {
  currentCompIndex++;
  if (currentCompIndex >= compList.length) {
    currentCompIndex = 0;
  }
  currentComp.value = compList[currentCompIndex];
  currentCompName.value = compNameList[currentCompIndex];
};
</script>

<template>
  <section>
    <h2>Slotの利用</h2>
    <OneSection v-bind:name="kazu">
      <p>{{ kazu }}さんは連絡がつきません。</p>
    </OneSection>
    <OneSection v-bind:name="taro">
      <template v-slot:default>
        <p>問題発生</p>
      </template>
      <template v-slot:detail>
        <ul>
          <li v-for="problem in taroProblems" v-bind:key="problem">{{ problem }}</li>
        </ul>
      </template>
    </OneSection>
    <OneSection v-bind:name="jiro" />
    <OneSection01 />
    <OneSection01>
      <template v-slot:default="slotProps">
        <dl>
          <dt>名前</dt>
          <dd>{{ slotProps.memberInfo.name }}</dd>
          <dt>状況</dt>
          <dd>{{ slotProps.memberInfo.state }}</dd>
        </dl>
      </template>
    </OneSection01>
  </section>

  <!-- 9.4.1 -->
  <p>コンポーネント名：{{ currentCompName }}</p>
  <KeepAlive>
    <component v-bind:is="currentComp" />
  </KeepAlive>
  <button v-on:click="switchComp">切り替え</button>
</template>
