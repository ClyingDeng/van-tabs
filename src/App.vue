<template>
  <div class="app">
    <h1>问题：</h1>
    <Promble />
    <h2>解决：</h2>
    <Result />
  </div>
</template>
<script>
import Promble from './components/Promble.vue'
import Result from './components/Result.vue'
export default {
  components: {
    Promble,
    Result,
  },
}
</script>
