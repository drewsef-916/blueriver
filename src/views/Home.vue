<template>
  <div class="home">
    <h1>Index</h1>
    <BuildingIndex />
  </div>
</template>

<script>
// @ is an alias to /src
import BuildingIndex from '@/components/BuildingIndex.vue'

export default {
  name: 'Home',
  components: {
    BuildingIndex
  }
}
</script>

<style lang="scss">

</style>
