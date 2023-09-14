<template>
  <div class="w-full flex flex-col items-center justify-between space-y-8">
    <h1 class="mt-40 font-bold tracking-tight text-white-900 sm:text-6xl">Chuckles with Dad</h1>
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
