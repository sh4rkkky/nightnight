<script setup>
import { ref } from 'vue';
import words from './assets/words.json'
let message = ref('กดสุ่มเลยเด้ ง่วง~')

const getLastCharactor = (str) => {
  return str[str.length-1]
}

const dobuleLastCharactor = (str, len) => {
  let lastChar = getLastCharactor(str);
  if (
    lastChar === "์" ||
    lastChar === "ี" ||
    lastChar === "ๆ" ||
    lastChar === "ู"
  ) {
    return str
  }
  let doubleChar = str + lastChar.repeat(len-1)
  return doubleChar
}

const orSpace = (str) => {
  let ran = Math.floor(Math.random() * 2);
  if (ran) {
    return str.replace("|", "")
  }
  return str.replace("|", " ")
}

const randomOfArray = (arr) => {
  let ran = Math.floor(Math.random() * (arr.length));
  return arr[ran]
}

const copyResult = () => {
  navigator.clipboard.writeText(message.value).then(() => {
    console.log('Content copied to clipboard');
  },() => {
    console.error('Failed to copy');
  });
}

const random = () => {
  let him = randomOfArray(words["him"]);
  let bye = orSpace(dobuleLastCharactor(randomOfArray(words["cya"]),Math.floor(Math.random() * 3) + 1))
  let goodnight = randomOfArray(words["goodnight"])
  let endidk = randomOfArray(words["endidk"])
  let emoji = randomOfArray(words["emoji"])
  let emoji2 = randomOfArray(words["emoji"])
  let love = orSpace(randomOfArray(words["love"]),2).replace("<him>", him)
  let end = randomOfArray(words["end"])

  

  let case1 = `${bye} ${goodnight}${endidk}${end}${him} ${love}${dobuleLastCharactor("~",1)} ${emoji}${emoji2}`;
  let case2 = `${goodnight}${dobuleLastCharactor(endidk, 2)} ${bye} ${love}${emoji}`
  let case3 = `${bye.replace(" ","")}${endidk}${him}${goodnight}${him}${dobuleLastCharactor("~",2)} ${emoji}`
  let case4 = `${goodnight}${dobuleLastCharactor(endidk,3)}${bye.replace(" ","")} ${love}${emoji}`

  let cases = [
    case1,
    case2,
    case3,
    case4,
  ]
  message.value = randomOfArray(cases);
}

</script>

<template>
  <div class="container mx-auto mt-[200px]">
    <div class="flex justify-center">
      <div class="flex flex-col">
        <h1 class="text-2xl mb-2">คุณอยากบอกฝันดีกับคุณที่รักในหลายๆ รูปแบบหรือเปล่า ? 💤</h1>
        <button @click="random" class="text-2xl bg-slate-600 hover:bg-slate-800 rounded-md border p-1 transition duration-150 hover:scale-105 hover:translate-y-1 delay-150 ">สุ่มเลย</button>
        <div class="flex flex-col justify-center">
          <p class="ml-3 mb-2 mt-6 text-xl">{{ message }}</p>
        </div>
        <button @click="copyResult" class="text-[16px] w-auto rounded bg-pink-300 hover:bg-pink-400 px-2 py-1 transition text-black">ก๊อปปี้</button>
      </div>
    </div>
  </div>
</template>
