<template>
  <div>
    <p>{{ getJoke }}</p>
    <button @click="getRandomJoke">New Joke</button>
    <button @click="addtoFavs(jokeId)"> Favorite Jokes</button>
    <ul v-for="fav in favJokesList" :key="fav.id">
      <li>{{ fav.joke }}</li>
    </ul>
  </div>
</template>

<script>
import { Buffer } from 'buffer';

export default {
  name: "Jokes",
  data() {
    return {
      getJoke: '',
      jokeId: '',
      gotJokeById: '',
      favJokesList: [],
      favJoke: '',
      error: null
    }
  },
  mounted() {
    Buffer
    this.getRandomJoke()
    this.getJokeById()
  },
  methods: {
    async getRandomJoke() {
      try {
        const response = await fetch("https://icanhazdadjoke.com/", {
          headers: {
            'Accept': 'application/json',
          },
        });
        const data = await response.json()
        this.getJoke = data.joke
        this.jokeId = data.id
      } catch (error) {
        console.error('Error fetching joke:', error);
        alert("Error fetching jokes")
      }
    },
    async getJokeById(jokeId) {
      try {
        const response = await fetch(`https://icanhazdadjoke.com/j/${jokeId}`, {
          headers: {
            'Accept': 'application/json',
          },
        });
        const data = await response.json()
        this.gotJokeById = data.joke
      } catch (error) {
        console.error('Error fetching joke:', error);
        alert("Error fetching jokes")
      }
    },
    addtoFavs(id) {
      if (id) {
        this.getJokeById(id)
        if (!this.favJokesList.includes(id)) {
          this.favJokesList.push({
            id: this.jokeId,
            joke: this.gotJokeById
          })
        }
      }
      console.log(this.favJokesList)
    }
  },
}
</script>

<style></style>