<template>
  <div>
    <div>{{ r1 }}</div>
    <div>{{ r2 }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch, watchEffect } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {
    function fetch(): Promise<string> {
      return new Promise(resolve => {
        setTimeout(() => {
          resolve("OK")
        }, 1000)
      })
    }

    const r1 = ref("--")
    const r2 = ref("--")

    fetch()
      .then(res => {
        r1.value = res
        r2.value = res
      })

    // https://v3.ja.vuejs.org/guide/reactivity-computed-watchers.html#watch
    watch(r1, r1 => {
      // OK のみ表示される
      console.log(`r1: ${r1}`)
    })

    // https://v3.ja.vuejs.org/guide/reactivity-computed-watchers.html#watcheffect
    watchEffect(() => {
      // -- と OK が表示される
      console.log(`r2: ${r2.value}`)
    })

    return {
      r1,
      r2,
    }
  },
})
</script>
