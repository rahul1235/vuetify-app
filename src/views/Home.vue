<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <AutoComplete/>
  </div>
</template>

<script>
// @ is an alias to /src
import AutoComplete from '@/components/AutoComplete.vue'

export default {
  name: 'home',
  components: {
    AutoComplete
  }
}
</script>
