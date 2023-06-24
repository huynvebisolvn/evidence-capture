<script setup lang="ts">
import { ref } from "vue"
import ArrowDown from './ArrowDown.vue';

const picturesRef: any = ref([])

const onDelete = (index: number) => {
  picturesRef.value.splice(index, 1)
  resetSeq()
}

const resetSeq = () => {
  picturesRef.value.sort((a, b) => a.seq - b.seq)
  for (let i = 0; i < picturesRef.value.length; i++) {
    picturesRef.value[i].seq = i + 1
  }
}

const pasteFunction = (pasteEvent: any, callback: any) => {
  if (pasteEvent.clipboardData == false) {
    if (typeof callback == "function") {
      console.log("Undefined ");
      callback(undefined);
    }
  }
  var items = pasteEvent.clipboardData.items;
  if (items == undefined) {
    if (typeof callback == "function") {
      callback(undefined);
      console.log("Undefined 2");
    }
  }
  for (var i = 0; i < items.length; i++) {
    if (items[i].type.indexOf("image") == -1) continue;
    var blob = items[i].getAsFile();
    const reader = new FileReader()
    reader.readAsDataURL(blob)
    reader.onload = ((e) => {
      if (e.target && e.target.result) {
        picturesRef.value.push({ seq: picturesRef.value.length + 1, img: e.target.result.toString() })
      }
    })
  }
}
</script>

<template>
  <div @paste="pasteFunction">
    <div v-if="picturesRef.length === 0" class="m-4 text-blue-500 text-4xl">Paste image</div>
    <div v-for="(picture, index) in picturesRef" :key="index" class="relative">
      <div class="relative flex items-center justify-center border border-slate-300 z-0">
        <div class="absolute top-0 right-0 bg-white rounded-md">
          <button class="ml-2 mr-2" @click="onDelete(index)">Step:</button>
          <input class="w-8 rounded-md" @change="resetSeq" v-model="picture.seq">
        </div>
        <img :src="picture.img" />
      </div>
      <ArrowDown v-if="index + 1 !== picturesRef.length"/>
    </div>
  </div>
</template>
