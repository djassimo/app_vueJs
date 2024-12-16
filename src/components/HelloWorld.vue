<script setup>
import { ref } from 'vue';

defineProps({
  msg: String,
  date: Date,
});
const currentDate = ref(new Date());

const count = ref(0);

const increment = () => {
  count.value++;
};

const decrement = () => {
  count.value--;
};

const movies = ref(['Top Gun', 'Gladiator', 'Pokemon']);

const deleteMovie = (movie) => {
  movies.value = movies.value.filter((m) => m !== movie);
};

const movieName = ref('');

const addMovie = (event) => {
  event.preventDefault();
  movies.value.push(movieName);
  //movieName.value = '';
};
</script>

<template>
  <h1>{{ msg }}</h1>
  <h3>{{ currentDate }}</h3>

  <div class="card">
    <p
      v-bind:id="`pointeur-${count}`"
      :style="{ color: count > 3 ? 'green' : 'red' }"
    >
      conteur : {{ count }}
    </p>

    <button type="button" @click="increment">Incrémenter</button>
    <button type="button" @click="decrement">Décrementer</button>
    <hr />

    <!--  
      - When i use "v-show a display none is added" 
      - If i choose "v-if" the element is removed from Dom
    -->
    <div v-if="count > 3">Bravo vous avez cliqué plus de 3 fois</div>

    <div v-else>Vous avez cliqué moins de 3 fois</div>
  </div>
  <div class="container">
    <div>
      <form action="" @submit.prevent="addMovie">
        <input
          type="text"
          placeholder="Nouveau film"
          v-model="movieName"
          required
       
          />
        <button>Ajouter</button>
      </form>
    </div>
    <ul>
      <li v-for="movie in movies">
        {{ movie }}
        <button @click="deleteMovie(movie)">Supprimer</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
