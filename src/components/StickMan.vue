<template>
<div>
  <div
    class="stickman"
    :style="{
      width: width + 'rem',
      height: height + 'rem'
    }"
  >
    <div
      class="head"
      :style="{
        height: headHeight + 'rem',
        width: headWidth + 'rem'
      }"
    ></div>
    <div class="torso">
      <div
        class="spine stick"
        :style="{
          transform: SpineAngle
        }"
        @click="setSpineAngle(30)"
      ></div>
      <div class="pelvic stick"></div>
    </div>
    <div class="handLeft"></div>
    <div class="handRight"></div>
    <div class="legs"></div>
  </div>
</div>
</template>

<script lang="ts">
import { defineComponent, computed, ref } from 'vue'

export default defineComponent({
  props: {
    width: {
      required: true,
      type: Number
    }
  },
  setup (props) {
    const height = computed(() => {
      return props.width * 3
    })

    const headHeight = computed(() => height.value * 0.11)
    const headWidth = computed(() => headHeight.value * 0.8)

    const spineAngle = ref(-30)
    const setSpineAngle = (angle:number) => {
      spineAngle.value = angle
    }
    const SpineAngle = computed(() => {
      return `rotate(${spineAngle.value}deg)`
    })

    return {
      height,
      headHeight,
      headWidth,
      setSpineAngle,
      SpineAngle
    }
  }
})
</script>

<style lang="scss" scoped>
  $head-height: 12%;
  $torso-height: 35%;
  $leg-height: 53%;
  .head {
    position: relative;
    background-color: black;
    border-radius: 50%;
  }
  .torso {
    position: relative;
    left: 7%;
    width: 14%;
    background-color: aquamarine;
  }

  .spine {
    position: relative;
    height: 200rem;
    left: 40%;
    transform-origin: 50% top;
  }
  .pelvic {
    position: relative;
    height: 100rem;
    transform-origin: 50% top;
    transform: rotate(30deg);
  }
  .legs {
    position: relative;
    height: $leg-height;
    width: 30%;
    background-color:bisque;
  }
</style>
