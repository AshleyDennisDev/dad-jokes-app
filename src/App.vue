<template>
  <div class="bg-stone-950	">
    <h1 class="text-4xl font-bold tracking-tight text-white-900 sm:text-6xl">Chuckles with Dad</h1>
    <Jokes/>
</div>
</template>

<script>
import Jokes from "./components/Jokes.vue";

export default{
  components: {
     Jokes,
  },
}
</script>

<style scoped>

</style>
