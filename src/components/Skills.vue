<template>
  <div class="hello">
    <form @submit.prevent="addSkill">
      <input autocomplete=false type="text" placeholder="Skriv in något du kan!" v-model="skill" v-validate="'min:2|max:29'" name="kunskaper"/>
      <transition name="fel">
        <p class="alert" v-if="errors.has('kunskaper')">Du måste ha mellan 2 och 29 tecken!</p>
      </transition>
    </form>
    <ul>
      <transition-group name="lista" enter-active-class="animated bounceInDown" leave-active-class="animated bounceOutDown">
        <li v-for="(data, index) in skills" :key="index">{{data.skill}}</li>
      </transition-group>
    </ul>
    <p v-if="skills.length < 1">Ånej, du kan ingenting!</p>
    <p v-else>Du kan de här sakerna.</p>
  </div> 
</template>
<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill: "",
      skills: [ 
      ],
      plac: "Skriv in någonting du kan!",
    }
  },
  "methods": {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if(result) {
          if(this.skill === "") {
            this.skills.pop();
          }
          else {
            this.skills.push({skill: this.skill});
            this.skill = "";
          }
        }
        else {
          console.log("Så där fär man inte göra");
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";

.holder {
    background: #fff;
  }
  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }
  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
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
    color: #687F7F;
  }
  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }
  .fel-enter-active {
    animation: strange .5s;
  }
  .fel-leave-active {
    animation: strange .5s reverse;
  }
  @keyframes strange {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.5);
    }
    100% {
      transform: scale(1);
    }

  }
</style>
