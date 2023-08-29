<template>
  <div>
    <div class="rounded-2xl bg-gray-50 py-10 text-center ring-1 ring-inset ring-gray-900/5 lg:flex lg:flex-col lg:justify-center lg:py-16">
            <div class="mx-auto max-w-xs px-8">
              <p class="text-base font-semibold text-gray-600 gap-x-2">{{ getJoke }}</p>
              <button class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600" @click="getRandomJoke">New Joke</button>
              <button class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600" @click="addToFavs(jokeId)"> Favorite Jokes</button>
            </div>
          </div>
    <ul role="list" class="divide-y divide-red-300" v-for="fav in favJokesList" :key="fav.id">
      <li class="flex justify-between gap-x-6 py-5">{{ fav.joke }}</li>
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

    async addToFavs(id) {
      await this.getJokeById(id)
      if (!this.favJokesList.includes(id)) {
        this.favJokesList.push({
          id: this.jokeId,
          joke: this.gotJokeById
        })
      }
    }
  },
}
</script>

<style></style>