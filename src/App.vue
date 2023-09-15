<template>
  <div class="w-full flex flex-col items-center justify-between space-y-6">
    <h1 class="mt-40 font-bold tracking-tight text-white-900 text-center text-3xl md:text-6xl">Chuckles with Dad</h1>
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

<style>

</style>
