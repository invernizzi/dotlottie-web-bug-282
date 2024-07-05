<template>
  <div>
    <canvas ref="canvasBroken" width="300" height="300" />
    <canvas ref="canvasWorking" width="300" height="300" />
  </div>
</template>


<script setup>
import { DotLottie } from "@lottiefiles/dotlottie-web";
import animationDataUrl from '@/public/animation.lottie?url';


const canvasBroken = ref()
const canvasWorking = ref()

/**
 * We load the animation using `src`. This works in dev but it's broken in prod.
 */
const brokenAnimation = () => {
  new DotLottie({
    canvas: canvasBroken.value,
    src: animationDataUrl,
    autoplay: true,
    loop: true,
  })
} 

/**
 * We load the animation using `data`, sidestepping the code that triggers the bug. 
 * This works everywhere.
 */
const workingAnimation = async () => {
  const response = await fetch(animationDataUrl)
  new DotLottie({
    canvas: canvasWorking.value,
    data:  await response.arrayBuffer(),
    autoplay: true,
    loop: true,
  })
}

onMounted(() => {
  workingAnimation();
  brokenAnimation();

})
</script>
