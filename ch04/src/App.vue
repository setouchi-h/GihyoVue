<script setup lang="ts">
import { ref, computed } from "vue";

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

const msg = ref("Hello Vue 3!");
const msgTextRed = ref("red");
const msgTextColor = ref("white");
const msgBgColor = ref("black");
const msgStyles = ref({
  color: "white",
  backgroundColor: "black"
});
const msgStyles2 = ref({
  fontSize: "24pt"
});
const msgStyles3 = ref({
  color: "pink",
  fontSize: "24pt"
});
const textSize = computed((): string => {
  const size = Math.round(Math.random() * 25) + 10;
  return `${size}pt`;
});

const isTextColorRed = ref(true);
const isBgColorBlue = ref(false);
const styles = ref({
  textColorRed: false,
  bgColorBlue: true
});
const computedStyles = computed((): { textColorRed: boolean; bgColorBlue: boolean } => {
  const randText = Math.round(Math.random());
  let textColorFlg = true;
  if (randText == 0) {
    textColorFlg = false;
  }

  const randBg = Math.round(Math.random());
  let bgColorFlg = true;
  if (randBg == 0) {
    bgColorFlg = false;
  }

  return {
    textColorRed: textColorFlg,
    bgColorBlue: bgColorFlg
  };
});

const randValue = ref("not clicked yet");
const onButtonClick = (): void => {
  const rand = Math.round(Math.random() * 10);
  randValue.value = rand.toString();
};

const mousePointerX = ref(0);
const mousePointerY = ref(0);
const onImgMousemove = (event: MouseEvent): void => {
  mousePointerX.value = event.offsetX;
  mousePointerY.value = event.offsetY;
};

const pBgColor = ref("white");
const onPClick = (bgColor: string) => {
  pBgColor.value = bgColor;
};

const pMsg = ref("イベント前（ここをクリック）");
const pBgColorEvent = ref("white");
const onPClickWithEvent = (bgColor: string, event: MouseEvent): void => {
  pBgColorEvent.value = bgColor;
  pMsg.value = event.timeStamp.toString();
};

const msgToSubmit = ref("未送信");
const onFormSubmit = (): void => {
  msgToSubmit.value = "送信されました";
};

const msgToShow = ref("まだです");
const onEnterKey = (): void => {
  msgToShow.value = "Enterキーが押下されました";
};
const onRightButtonClick = (): void => {
  msgToShow.value = "右クリックされました";
};
const onShiftClick = (): void => {
  msgToShow.value = "シフトを押しながらクリックされました";
};
</script>

<template>
  <p><a v-bind:href="url" target="_blank">Vue.jsのサイト</a></p>
  <p><a :href="url" target="_blank">Vue.jsのサイト（省略形）</a></p>
  <p><a v-bind:href="url + 'guide/introduction.html'">vue.jsガイドページ</a></p>
  <p><button type="button" v-bind:disabled="isSendButtonDisabled">送信</button></p>
  <p><img alt="VueLogo" src="./assets/logo.svg" v-bind:[widthOrHeight]="widthOrHeightValue" /></p>
  <p><img v-bind="imageAttributes" /></p>
  <p><img v-bind="imageAttributes" title="ロゴです！" /></p>
  <p><img v-bind="imageAttributes" alt="ロゴです" /></p>

  <p v-bind:style="{ color: msgTextRed }">{{ msg }}</p>
  <p v-bind:style="{ color: 'pink' }">{{ msg }}</p>
  <p v-bind:style="{ fontSize: textSize }">{{ msg }}</p>
  <p v-bind:style="{ color: msgTextColor, backgroundColor: msgBgColor }">{{ msg }}</p>
  <p v-bind:style="{ color: msgTextColor, 'background-color': msgBgColor }">{{ msg }}</p>
  <p v-bind:style="msgStyles">{{ msg }}</p>
  <p v-bind:style="[msgStyles, msgStyles2]">{{ msg }}</p>
  <p v-bind:style="[msgStyles, msgStyles3]">{{ msg }}</p>
  <p v-bind:style="[msgStyles3, msgStyles]">{{ msg }}</p>

  <p v-bind:class="{ textColorRed: true, bgColorBlue: true }">{{ msg }}</p>
  <p v-bind:class="{ textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue }">{{ msg }}</p>
  <p v-bind:class="{ textColorPink: true }">{{ msg }}</p>
  <p v-bind:class="{ 'text-color-pink': true }">{{ msg }}</p>
  <p class="textSize24" v-bind:class="{ textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue }">
    {{ msg }}
  </p>
  <p class="textSize24" v-bind:class="styles">{{ msg }}</p>
  <p v-bind:class="computedStyles">{{ msg }}</p>

  <section>
    <button v-on:click="onButtonClick">Click</button>
    <p>クッリクの結果：{{ randValue }}</p>
  </section>

  <section>
    <img src="./assets/logo.svg" alt="Vueのロゴ" width="200" v-on:mousemove="onImgMousemove" />
    <p>ポインタの位置：x={{ mousePointerX }}; y={{ mousePointerY }}</p>
  </section>

  <p v-on:click="onPClick('red')" v-bind:style="{ backgroundColor: pBgColor }">
    ここをクリックすると背景色が変わります
  </p>
  <p
    v-on:click="onPClickWithEvent('green', $event)"
    v-bind:style="{ backgroundColor: pBgColorEvent }"
  >
    {{ pMsg }}
  </p>

  <form action="#" v-on:submit.prevent="onFormSubmit">
    <input type="text" required />
    <button type="submit">送信</button>
  </form>
  <p>{{ msgToSubmit }}</p>

  <p>{{ msgToShow }}</p>
  <input type="text" v-on:keydown.enter.exact="onEnterKey" /><br />
  <button v-on:click.right="onRightButtonClick">右クリック</button><br />
  <button v-on:click.shift="onShiftClick">シフトを押しながらクリック</button>
</template>

<style>
.textColorRed {
  color: red;
}
.text-color-pink {
  color: pink;
}
.bgColorBlue {
  background-color: blue;
}
.textSize24 {
  font-size: 24px;
}
</style>
