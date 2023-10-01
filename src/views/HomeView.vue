<template>
  <div class="container">
    <Plan msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Plan from '@/components/Plan.vue'

export default {
  name: 'HomeView',
  components: {
    Plan
  }
}
</script>
