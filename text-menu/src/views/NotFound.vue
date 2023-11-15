<template>
  <div style="text-align: center;">
    <h1>Not Found</h1>
    <p>
      <a href="https://www.greatmenucovers.com">Go Home?</a>
    </p>
  </div>

</template>

<script>
import {defineComponent} from "vue";
import {useRoute} from "vue-router";

export default defineComponent({
  name: 'NotFound',
  setup() {
    const route = useRoute()
    return { route }
  }
})

</script>

<style scoped>

</style>
