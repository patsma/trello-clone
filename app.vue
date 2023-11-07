<template>
  <div class="h-full overflow-auto  px-8 ">
    <div class="loader-group absolute overflow-hidden z-[-1] h-full w-full">
      <div
          class="loader"
          style="
          background-image: radial-gradient(circle, #ffc8c4, rgb(247, 247, 247), rgb(245, 248, 245));
          width: 100vw;
          height: 100vh;
          position: fixed;
          z-index: 10;
          animation: fade-in-out 20s infinite linear;
          transform: scale(1);
        "
      ></div>
      <div id="loader-wrapper">
        <svg style="opacity: 0.6" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <radialGradient cx="0.5" cy="0.5" id="blobGradient" r="0.5">
              <stop offset="0%" style="stop-color: #ffebcd"></stop>
              <stop offset="100%" style="stop-color: #ffc7b4"></stop>
            </radialGradient>
          </defs>
          <path
              d="M40.1,-46.6C49,-40.3,51.3,-24.9,50.7,-11.4C50.2,2.1,46.8,13.6,40.2,21.5C33.6,29.4,23.7,33.7,11.7,42.6C-0.3,51.5,-14.5,65.1,-27.6,65C-40.8,64.9,-52.9,51.2,-57.7,36.5C-62.4,21.7,-59.8,5.8,-58.8,-12.2C-57.8,-30.2,-58.5,-50.4,-49,-56.7C-39.5,-63,-19.7,-55.4,-2.1,-52.9C15.6,-50.4,31.1,-53,40.1,-46.6Z"
              fill="url(#blobGradient)"
              id="blob"
              transform="translate(100 100)"
          />
        </svg>
      </div>
    </div>
    <div class="grid justify-center p-10">
      <a href="https://tastysites.pl" target="_blank">
        <img class="h-full w-80" src="@/assets/img/tastylogo.svg" alt="" />
      </a>
    </div>
    <TrelloBoard />
  </div>
</template>
<style>
html,body{
  overflow-x: hidden;
}
/* This styles the scrollbar track */
::-webkit-scrollbar {
  height: 10px; /* height of the horizontal scrollbar */
  background: rgba(241, 241, 241, 0.44); /* color of the scrollbar track */
}

/* This styles the scrollbar handle */
::-webkit-scrollbar-thumb {
  background: rgba(136, 136, 136, 0.57); /* color of the scrollbar handle */
  border-radius: 16px; /* roundness of the scrollbar handle */
}



#loader-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  transform-origin: 50% 50%;
  transform: scale(2);
}

#loader-wrapper svg {
  width: 300px;
  height: 300px;
  transform-origin: 50% 50%;
}

@keyframes initialRotate {
  0% {
    transform: translate(2.5%,0) rotate(0deg) scale(2);
  }
  100% {
    transform: translate(0,0) rotate(720deg) scale(2.25);
  }
}

#loader-wrapper {
  animation: initialRotate 40s linear infinite alternate;
}

@keyframes fade-in-out {
  0% {
    transform: scale(2);
  }
  50% {
    transform: scale(4);
  }
  100% {
    transform: scale(2);
  }
}
</style>
<script setup lang="ts">
import gsap from "gsap";
import { MorphSVGPlugin } from 'gsap/MorphSVGPlugin';
gsap.registerPlugin(MorphSVGPlugin);

useHead({
  title: 'Tasty Trello Board Clone',
})
function loaderBlob() {
  const tl = gsap.timeline({ repeat: -1 });
  const blob = document.querySelector("#blob");

  const randomizeBlob = (function () {
    const shapes = [
      "M45.2,-58.1C57.2,-43.8,64.5,-28.2,69.8,-10.5C75.2,7.3,78.5,27.3,70.3,39.7C62.1,52.1,42.3,56.9,23.1,64.3C3.9,71.7,-14.7,81.6,-28.1,76.9C-41.5,72.1,-49.7,52.8,-58.2,35C-66.8,17.3,-75.7,1.2,-69.1,-7.9C-62.4,-17,-40.1,-19.2,-26,-33C-11.9,-46.9,-5.9,-72.5,5.3,-78.9C16.6,-85.2,33.2,-72.3,45.2,-58.1Z",
      "M24.6,-30.5C31.9,-23.1,37.9,-15.4,42.7,-5.1C47.4,5.3,50.9,18.4,46.5,27.5C42,36.7,29.6,42,18.2,43.1C6.9,44.2,-3.5,41.1,-10.3,35.5C-17.1,29.9,-20.4,21.8,-27.6,13.8C-34.8,5.8,-45.8,-2.1,-52.4,-17C-59,-31.8,-61.1,-53.6,-51.6,-60.6C-42.2,-67.6,-21.1,-59.8,-6.2,-52.3C8.6,-44.9,17.2,-37.9,24.6,-30.5Z",
      "M32.8,-37.9C48.2,-26.2,70.2,-21.2,76.7,-9.8C83.2,1.6,74,19.6,60.2,26.4C46.3,33.2,27.6,28.8,12.7,33.8C-2.2,38.8,-13.4,53.2,-28.4,56.9C-43.4,60.6,-62.2,53.7,-71,40.2C-79.8,26.7,-78.6,6.5,-74.8,-12.9C-71,-32.3,-64.7,-50.9,-51.8,-63C-38.9,-75,-19.4,-80.6,-5.4,-74.2C8.7,-67.8,17.5,-49.5,32.8,-37.9Z",
      "M30.8,-30.4C41.6,-27.6,53.4,-19.5,59.2,-7.4C65.1,4.8,65,21.2,56.3,29C47.6,36.8,30.3,36.2,15.8,40C1.3,43.9,-10.4,52.2,-20,50.6C-29.6,49,-37.1,37.4,-39.8,26.2C-42.4,15,-40.2,4.1,-37.3,-5.7C-34.5,-15.5,-31.2,-24.3,-24.8,-27.9C-18.5,-31.5,-9.3,-29.9,0.4,-30.3C10,-30.7,19.9,-33.2,30.8,-30.4Z",
      "M53.5,-59C65.5,-53.6,68.8,-33.2,65.2,-16.9C61.5,-0.7,51,11.3,42.7,23.7C34.4,36,28.4,48.7,17.8,55.2C7.3,61.8,-7.7,62.2,-23.8,59.1C-39.9,56,-57,49.4,-64.5,37C-72,24.5,-69.8,6.3,-61.2,-5.2C-52.5,-16.7,-37.2,-21.4,-25.9,-26.9C-14.6,-32.5,-7.3,-38.8,6.7,-46.8C20.7,-54.7,41.4,-64.4,53.5,-59Z",
      "M36.9,-42.2C50.6,-32.6,66.2,-23.5,66.9,-12.8C67.6,-2.1,53.3,10.2,43.6,23.3C33.8,36.3,28.5,50,18,57.1C7.5,64.2,-8.1,64.8,-25.6,62C-43.1,59.2,-62.3,53.2,-72.7,39.8C-83,26.4,-84.4,5.6,-79.3,-12.3C-74.1,-30.3,-62.5,-45.4,-48.2,-55C-33.9,-64.5,-17,-68.4,-2.7,-65.2C11.6,-62,23.3,-51.8,36.9,-42.2Z",
      "M39.8,-46.2C47.4,-41,46.6,-24.5,48,-9.5C49.4,5.5,53.1,19.1,47.2,25.3C41.3,31.5,25.9,30.2,10.9,40C-4.1,49.9,-18.8,70.8,-31.5,72.4C-44.3,73.9,-55.2,56.1,-55.3,39.8C-55.3,23.5,-44.5,8.8,-38.5,-3.6C-32.5,-15.9,-31.2,-25.8,-25.6,-31.3C-20,-36.9,-10,-38,3,-41.7C16.1,-45.3,32.1,-51.4,39.8,-46.2Z",
    ];

    let lastShapeIndex = null;

    return function () {
      let newIndex;
      do {
        newIndex = Math.floor(Math.random() * shapes.length);
      } while (newIndex === lastShapeIndex);

      lastShapeIndex = newIndex;
      return shapes[newIndex];
    };
  })();

  const gradientStops = document.querySelectorAll("#blobGradient stop");
  const colors = [
    ["#19FFF1", "#875EFF", "#FFCD1E", "#FF0A7F"],
    ["#FF33CC", "#FF00FF", "#FF6699", "#FF99CC"],
    ["#FF00FF", "#FF33CC", "#FF9999", "#FF6699"],
    ["#FF6699", "#FF00FF", "#FF33CC", "#FF99CC"],
  ];

  function animateTogether() {
    const nextShape = randomizeBlob();

    // Animate blob shape
    gsap.to(blob, {
      morphSVG: nextShape,
      duration: 6,
      ease: "linear",
      overwrite: "auto",
    });

    // Animate gradient colors
    gradientStops.forEach((stop, index) => {
      const currentColor = stop.getAttribute("style").split(":")[1].slice(0, -1).trim();
      let nextColorIndex;
      do {
        nextColorIndex = Math.floor(Math.random() * colors[index].length);
      } while (colors[index][nextColorIndex] === currentColor);
      gsap.to(stop, {
        attr: { style: `stop-color:${colors[index][nextColorIndex]};` },
        duration: 1.8,
        ease: "sine.inOut",
        overwrite: "auto",
      });
    });

    gsap.delayedCall(5, animateTogether);
  }

  animateTogether();
}
onMounted(() => {
  loaderBlob();
});

</script>
