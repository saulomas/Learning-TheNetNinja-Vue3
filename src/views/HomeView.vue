<template>
  <div class="home">
    <h1>Home</h1>
    <input type="text" v-model="search">
    <p>Search term: {{ search }}</p>
    <table class="center">
      <tr>
        <td>
          <div v-for="name in names" :key="name">{{ name }}</div>
        </td>
        <td>
          <div v-for="name in matchingNames" :key="name">{{ name }}</div>
        </td>
      </tr>
    </table>
    <button @click="handleClick">Stop Watching</button>
  </div>
</template>

<script>
import { computed, ref, watch, watchEffect } from 'vue'

export default {
  name: 'HomeView',
  setup() {
    const search = ref('')
    const names = ref(['mario', 'yoshi', 'luigi', 'toad', 'bowser', 'koopa', 'peach'])

    const stopWatch = watch(search, () => {
      console.log('Watch function ran')
    })

    const stopEffect = watchEffect(() => {
      console.log('WatchEffect runction ran', search.value)
    })

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value))
    })

    const handleClick = () => {
      stopWatch()
      stopEffect()
    }

    return { names, search, matchingNames, handleClick }
  }
}
</script>

<style>
.center {
  margin-left: auto;
  margin-right: auto;
}
</style>
