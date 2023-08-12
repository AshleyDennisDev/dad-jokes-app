<template>
    <div>
        <p>{{ getJoke }}</p>
        <button @click="getRandomJoke">New Joke</button>
    </div>
</template>

<script>
export default{
    name: "Jokes",
    data () {
    return {
      getJoke: '',
      error: null
    }
  },
  mounted(){
    this.getRandomJoke()
  },
  methods: {
    async getRandomJoke() {
        try{
        const response = await fetch("https://icanhazdadjoke.com/",{
          headers: {
            'Accept': 'application/json',
          },
        });
        const  data  = await response.json()
        this.getJoke = data.joke
        }catch (error){
            console.error('Error fetching joke:', error);
            alert("Error fetching jokes")  
        }
    }

  },
}
</script>

<style>
</style>