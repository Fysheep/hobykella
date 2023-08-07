<script lang="ts">
import raum from "@/assets/icons/raum.png"
import bank from "@/assets/icons/bank1.png"
import bankEck1 from "@/assets/icons/bankEck1.png"
import bankEck2 from "@/assets/icons/bankEck2.png"
import bankKeineLehne from "@/assets/icons/bankKeineLehne.png"
import bankShort1 from "@/assets/icons/bankShort1.png"
import bankShort2 from "@/assets/icons/bankShort2.png"
import cocktailTisch from "@/assets/icons/cocktailTisch.png"
import glasTisch from "@/assets/icons/glasTisch.png"
import kasten from "@/assets/icons/kasten.png"
import muschel from "@/assets/icons/muschel.png"
import rezeption from "@/assets/icons/rezeption.png"
import sessel from "@/assets/icons/sessel.png"
import zapfsaeule from "@/assets/icons/zapfseule.png"
import box1 from "@/assets/icons/box1.png"
import box2 from "@/assets/icons/box2.png"

export default {
  data() {
    return {
      images: JSON.parse(localStorage.getItem("speicher")!) ?? [
        { src: raum, pos: { x: 100, y: 100 }, width: 520, height: 730, rotation: 0 },
        { src: zapfsaeule, pos: { x: 100, y: 100 }, width: 60, height: 80, rotation: 0 },
        { src: muschel, pos: { x: 100, y: 100 }, width: 100, height: 170, rotation: 0 },
        { src: cocktailTisch, pos: { x: 100, y: 100 }, width: 100, height: 180, rotation: 0 },
        { src: rezeption, pos: { x: 100, y: 100 }, width: 120, height: 45, rotation: 0 },
        { src: kasten, pos: { x: 100, y: 100 }, width: 60, height: 210, rotation: 0 },
        { src: glasTisch, pos: { x: 100, y: 100 }, width: 80, height: 60, rotation: 0 },
        { src: bankShort1, pos: { x: 100, y: 100 }, width: 90, height: 60, rotation: 0 },
        { src: bankShort2, pos: { x: 100, y: 100 }, width: 90, height: 60, rotation: 0 },
        { src: bankKeineLehne, pos: { x: 100, y: 100 }, width: 60, height: 90, rotation: 0 },
        { src: bankEck1, pos: { x: 100, y: 100 }, width: 90, height: 90, rotation: 0 },
        { src: bankEck2, pos: { x: 100, y: 100 }, width: 90, height: 90, rotation: 0 },
        { src: sessel, pos: { x: 100, y: 100 }, width: 85, height: 85, rotation: 0 },
        { src: bank, pos: { x: 100, y: 100 }, width: 90, height: 90, rotation: 0 },
        { src: box1, pos: { x: 100, y: 100 }, width: 30, height: 29, rotation: 0 },
        { src: box2, pos: { x: 100, y: 100 }, width: 30, height: 29, rotation: 0 },

      ] as Array<any>,
      dragObject: {} as any,
    }
  },
  methods: {
    drag(e: DragEvent, img: any) {
      this.dragObject = img;
    },
    over(e: DragEvent) {
      this.dragObject.pos.x = e.clientX - (this.dragObject.width / 2);
      this.dragObject.pos.y = e.clientY - (this.dragObject.height / 2);
      localStorage.speicher = JSON.stringify(this.images)
    },
    rotate(img: any) {
      img.rotation = img.rotation % 360 == 0 ? 315 : (img.rotation - 45);
    },
    rotateR(img: any) {
      
      img.rotation = img.rotation % 360 == 0 ? 45 : (img.rotation + 45);
    },
    clear() {
      localStorage.clear()
      location.reload()
    }
  }
}
</script>

<template>
  <div class="CONTENT" @dragover="over">
    <div v-for="img in images" class="fit"
      :style="`height: ${img.height}px; width: ${img.width}px; top: ${img.pos.y}px; left: ${img.pos.x}px; transform: rotateZ(${img.rotation}deg)`"
      @click="rotate(img)" @contextmenu.prevent="rotateR(img)">
      <img :src="img.src" alt="Fick Dich" draggable="false">
      <div draggable="true" class="filler" @dragstart="drag($event, img)" />
    </div>


    <button @click="clear">clear</button>
  </div>
</template>

<style scoped>
button {
  position: fixed;
  right: 0;
  bottom: 0;
}

.fit {
  position: absolute;
}

.fit:hover {
  cursor: grab;
  resize: both;
  outline: slateblue 1px solid;
}

img {
  resize: both;
  user-select: none;
}

.filler {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
}
</style>