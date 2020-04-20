<template>
  <div>
    <transition-group name="slideContainer" mode="out-in">
      <component
        key="mainContainer"
        @activeComponent="activeComponent= $event"
        :is="activeComponent"
      ></component>
      <canvas v-show="activeComponent == 'Celebrate'" key="canvasContainer" id="canvas"></canvas>
    </transition-group>

  </div>

</template>

<script>
  import Celebrate from './components/Celebrate';
  import Fail from './components/Fail';
  import GameCards from './components/GameCards';


  export default {
    name: 'app',
    components: {Celebrate, Fail, GameCards},
    data() {
      return {
        activeComponent: GameCards
      }
    }
  }
</script>

<style>
  body {
    font-family: sans-serif;
  }

  .slideContainer-enter {

  }

  .slideContainer-enter-active {
   animation: slide-in .3s ease-out forwards;
  }

  .slideContainer-leave {

  }

  .slideContainer-leave-active {
 animation: slide-out .3s ease-out forwards;
  }

  @keyframes slide-in {
    from {
      transform: translateX(-1000px);
      opacity: 1;
    }
    to {
      transform: translateX(0px);
      opacity: 0;
    }

  }
  @keyframes slide-out {
    from {
      transform: translateX(0px);
      opacity: 1;
    }
    to {
      transform: translateX(1000px);
      opacity: 0;
    }

  }
</style>
