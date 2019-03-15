<template>
  <div class="home">
    <Gubben/>
  </div>
</template>

<script>
// @ is an alias to /src
import Skills from '@/components/Skills.vue'
import Gubben from '@/components/Gubben.vue'

export default {
  name: 'home',
  components: {
    Skills,
    Gubben
  }
}
</script>
