<template>
  <div class="hello">
    <audio @canplay="dance" autoplay v-if="classCSS === 'dansa' || classCSS === 'dans'">
      <source src="..\\assets\\yakety_sax.mp3" type="audio/mpeg">
    </audio><br>
    <form @submit.prevent="command">
      <input type="text" placeholder="Vad ska han göra?" v-model="todo">
    </form>
    <input  type="text" placeholder="Vad heter han?" v-model="namnet">
    <br>
    <transition v-bind:name="classCSS">
      <div class="inline" @animationend="reset()" v-if="classCSS !== '' && classCSS !== 'dansa'" key="om">
        {{ namnet }}
        <br>
        <img src="..\assets\gubbe.png">
      </div>
      <div v-else key="annars">
        {{ namnet }}
        <br>
        <img src="..\assets\gubbe.png">
      </div>
    </transition>
    <transition v-bind:name="classCSSLady">
      <div class="inline" v-if="classCSSLady === 'dansDam'" key="gumma">
        {{ namnet.lastIndexOf("s") + 1 == namnet.length ? namnet + " fru" : namnet + "s fru" }}
        <br>
        <img src="..\assets\dam.png" width=224 height=225>
      </div>
    </transition>
    <div class="inline food_container">
      <transition style="display:inline;" v-bind:name="classCSSMat">
        <div @animationend="reset()" v-if="classCSSMat === 'ataMat'" key="mat">
          🍔
        </div>
      </transition>
    </div>
    <br>
    <transition name="sang">
      <div class="inline layer" key="sang" v-if="classCSS === 'sova'">
        <img src="..\assets\sang.png">
      </div>
    </transition>
  </div>
</template>
<script>
export default {
  name: "Gubben",
  data() {
    return {
      todo: "",
      classCSS: "",
      classCSSLady: "",
      classCSSMat: "",
      bild: "..\\assets\\gubbe.png",
      namnet: "Gamle Tiburtius",
      danssteg: 0
    };
  },
  methods: {
    command() {
      if (this.todo === "hoppa högt") {
        this.classCSS = "hoppahogt";
        return;
      }
      if (this.todo === "hoppa") {
        this.classCSS = "hoppa";
        return;
      }
      if (this.todo === "stretcha") {
        this.classCSS = "stretch";
        return;
      }
      if (this.todo === "ramla" || this.todo === "trilla") {
        this.classCSS = "ramla";
        return
      }
      if (this.todo === "falla") {
        this.classCSS = "falla";
        return;
      }
      if (this.todo === "snurra") {
        this.classCSS = "snurra";
        return;
      }
      if (this.todo === "do a barrel roll") {
        this.classCSS = "barrelRoll";
        return;
      }
      if (this.todo === "dansa") {
        this.classCSS = "dansa";
        this.danssteg = 0;
        return;
      }
      if (this.todo === "äta") {
        this.classCSS = "ata";
        this.classCSSMat = "ataMat";
        return;
      }
      if (this.todo === "sova") {
        this.classCSS = "sova";
        return;
      }
      this.classCSS = "";
      this.classCSSLady = "";
      this.classCSSMat = "";
    },
    reset() {
      if(this.classCSS !== "dans") {
        this.classCSS = "";
        this.classCSSLady = "";
        this.classCSSMat = "";
      }
      else {
        if(this.danssteg == 14) {
          this.classCSS = "";
          this.classCSSLady = "";
          this.classCSSMat = "";
        }
        else {
          this.danssteg = this.danssteg + 1;
        }
      }
    },
    dance() {
      this.classCSS = "dans";
      this.classCSSLady = "dansDam";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

.holder {
  background: #fff;
}
.dansDam {
  position: relative;
  top: 20px;
  right: 30px;
}
.inline {
  display: inline-block;
  position: relative;
}
ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}
div {
  text-align: center;
  padding: 30px 0;
  color: gray;
}
.layer {
  z-index: -1;
}
.container {
  box-shadow: 0px 0px 40px lightgray;
}
input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}
.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
}
.hoppa-enter-active {
  animation: jump 1s;
}
.hoppahogt-enter-active {
  animation-name: jump_high;
  animation-duration: 10s;
  animation-fill-mode: forwards;
}
.stretch-enter-active {
  animation: stretch 3s;
}
.falla-enter-active {
  animation: fall 10s;
}
.ramla-enter-active {
  animation: ramla 6s;
}
.snurra-enter-active {
  animation: flip 1s;
}
.barrelRoll-enter-active {
  animation-name: barrel_roll;
  animation-duration: 2s;
}
.dans-enter-active {
  animation: flip 1s, flip 1s linear 1s, jump 1s linear 3s, flip 1s linear 4s, swing 1s linear 5s, swing 1s linear 6s, wobble 1s linear 7s, swing 1s linear 8s, swing 1s linear 9s, wobble 1s linear 10s, stretch 5s linear 11s, swing 1s linear 16s, swing 1s linear 17s, barrel_roll 1s linear 18s, ramla 10s linear 19s;
}
.dansDam-enter-active {
  animation: hide 6s, dance_enter 2s ease-out 6s, stretch 5s linear 11s, swing 1s linear 16s, swing 1s linear 17s, barrel_roll 1s linear 18s, dance_leave 2s reverse 27s;
}
.ataMat-enter-active {
  animation: roll_scale_in 5s linear;
}
.sang-enter-active {
  animation: popup 20s linear;
}
.sova-enter-active {
  animation: sov 20s linear;
}
@keyframes jump {
  0% {
    animation-timing-function: linear;
    transform: translateY(0px);
  }
  50% {
    animation-timing-function: linear;
    transform: translateY(-100px);
  }
  100% {
    animation-timing-function: linear;
    transform: translateY(0px);
  }
}
@keyframes jump_high {
  0% {
    transform: translateY(0px);
  }
  6.125% {
    transform: translateY(-1000px);
  }
  12.5% {
    transform: translateY(0px);
  }
  25% {
    transform: translateX(-20px) translateY(50px) rotateZ(90deg);
  }
  50% {
    transform: translateX(-20px) translateY(50px) rotateZ(90deg);
  }
  100% {
    animation-timing-function: ease-out;
    transform: translateY(0px) rotateZ(0deg);
  }
}
@keyframes fall {
  from {
    animation-timing-function: ease-out;
    transform: translateY(0px);
  }
  2% {
    transform: translateY(1000px);
  }
  to {
    animation-timing-function: ease-out;
    transform: translateY(0px);
  }
}
@keyframes stretch {
  from {
    transform: scale3d(1, 1, 1);
  }
  30% {
    transform: scale3d(1.25, 0.75, 1);
  }

  40% {
    transform: scale3d(0.75, 1.25, 1);
  }

  50% {
    transform: scale3d(1.15, 0.85, 1);
  }

  65% {
    transform: scale3d(0.95, 1.05, 1);
  }

  75% {
    transform: scale3d(1.05, 0.95, 1);
  }

  to {
    transform: scale3d(1, 1, 1);
  }
  from,
  11.1%,
  to {
    transform: translate3d(0, 0, 0);
  }

  22.2% {
    transform: skewX(-12.5deg) skewY(-12.5deg);
  }

  33.3% {
    transform: skewX(6.25deg) skewY(6.25deg);
  }

  44.4% {
    transform: skewX(-3.125deg) skewY(-3.125deg);
  }

  55.5% {
    transform: skewX(1.5625deg) skewY(1.5625deg);
  }

  66.6% {
    transform: skewX(-0.78125deg) skewY(-0.78125deg);
  }

  77.7% {
    transform: skewX(0.390625deg) skewY(0.390625deg);
  }

  88.8% {
    transform: skewX(-0.1953125deg) skewY(-0.1953125deg);
  }
}
@keyframes ramla {
  0% {
    transform-origin: top left;
    animation-timing-function: ease-in-out;
  }
  5%,
  15% {
    transform: rotate3d(0, 0, 1, 80deg);
    transform-origin: top left;
    animation-timing-function: ease-in-out;
  }
  10%,
  20% {
    transform: rotate3d(0, 0, 1, 60deg);
    transform-origin: top left;
    animation-timing-function: ease-in-out;
  }

  25% {
    transform: translate3d(0, 700px, 0);
  }
  26% {
    transform: translate3d(0, 2000px, 0);
  }
  to {
    transform: translate3d(0, 0px, 0);
  }
}
@keyframes barrel_roll {
  from {
    transform: rotateZ(0deg);
    animation-timing-function: linear;
  }
  to {
    transform: rotateZ(360deg);
    animation-timing-function: linear;
  }
}
@keyframes dance_enter {
  from {
    transform: translateX(1000px);
  }
  to {
    transform: translateX(0px);
  }
}
@keyframes dance_leave {
  from {
    transform: translateX(1000px) scaleX(-1);
  }
  90% {
    transform: scaleX(-1);
  }
  to {
    transform: translateX(0px) scaleX(1);
  }
}
@keyframes hide {
  from {
    transform: translateX(1000px);
  }
  to {
    transform: translateX(1000px);
  }
}
@keyframes roll_scale_in {
  from {
    transform: translate(1000px, -160px) scale(1, 1);
    opacity: 0;
  }
  to {
    transform: translate(-100px, -160px) scale(1.1, 1.1);
    opacity: 1;
  }
}
@keyframes popup {
  from {
    transform: translateY(0px);
  }
  1% {
    transform: translateY(-480px);
  }
  2% {
    transform: translateY(-430px);
  }
  98% {
    transform: translateY(-430px);
  }
  99% {
    transform: translateY(-480px);
  }
  to {
    transform: translateY(0px);
  }
}
@keyframes sov {
  from {
    transform: skewX(0deg);
  }
  10% {
    transform: skewX(45deg);
  }
  90% {
    transform: skewX(45deg);
  }
  to {
    transform: skewX(0deg);
  }
}
</style>
