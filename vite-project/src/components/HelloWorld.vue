    
<script setup>
   import { ref } from "vue";
   import axios from "axios"
   const Movies = ref("");
   const response = ref(null);
    
   const getMovies = async () => {
   console.log(Movies.value)
   console.log(response.value)
   response.value = (await getData(`https://api.themoviedb.org/3/movie/${Movies.value}`, {
     params: {
       api_key: "354ab13223b58e3243b70a0085da1b2e",
   }
 })).data
}
    
const getData = async (url, params) => {
   try {
      return await axios.get(url, params);
    } catch (error) {
       console.log(error)
   }
};

</script>

<template>
  <div id="div1" :style="{'background-image':'url(https://images.pexels.com/photos/7605490/pexels-photo-7605490.jpeg?auto=compress&cs=tinysrgb&dpr=3&h=750&w=1260)'}">
    <h1 id="movies"> Movies </h1>
    <label id="label" for="Movies">Select Movies here:</label>
    <select name="Movies" id="Movies" v-model="Movies">
    <option value="384018">Fast and Furious 9</option>
    <option value="497698">Black Widow</option>
    <option value="634649">Spider-Man: No Way Home</option>
    <option value="438148">Minions: The Rise of Gru</option>
    <option value="512195">Red Notice</option>
    <option value="455207">Crazy Rich Asians</option>
    <option value="705861">Hustle</option>
    <option value="772">Home Alone 2: Lost in New York</option>
    <option value="284054">Black Panther</option>
    <option value="864">Cool Runnings</option>  
    </select>
    <button id=get @click="getMovies()">Get</button>
  <div v-if="response" class="Movies">
      <h1 id="title">Title: {{ response.title }}</h1>
      <p id="runtime">Runtime: {{ response.runtime }}</p>
      <p id="overview">Overview: {{ response.overview }}</p>
      <p id="release_date">Release date: {{ response.release_date }}</p>
      <p id="tagline"> {{ response.tagline }}</p>
      <p id="vote_count">Vote Count: <br>{{ response.vote_count }}</p>
      <p id="vote_average">Vote Average: <br>{{ response.vote_average }}</p>
      <p id="popularity">Popularity: <br>{{ response.popularity }}</p>
      <p id="revenue">Revenue: $ {{ response.revenue }}</p>
      <img v-bind:src="'https://image.tmdb.org/t/p/w500' + response.poster_path" /> 
    <div v-for="genre in response.genres">
      <p>{{ genre.name }}</p>
  </div>
  </div>
  </div>
</template>
 
<style>
p {
  font-family: 'Montserrat', sans-serif;
  color: #F1EEE9;
  text-align: right;
 }

#div1 > #movies {
    color: #F1EEE9;
    font-family: 'Merriweather', serif;
    font-size: 100px;
    text-align: center;
    padding-left: 8rem;
    padding-bottom: 1rem;
}
#div1 > #label {
    display: flex;
    color: #F1EEE9;
    font-family: 'Merriweather', serif;
    font-size: 30px;
    text-align: center; 
    justify-content: center;
    position: relative;
    left: 35rem;
    bottom: 20px;
}

#div1 > #label, #get, #Movies {
    display: inline;
}

#get, #Movies {
  display: flex;
  font-family: 'Merriweather', serif;
  font-size: 25px;
  text-align: center;
  justify-content: center;
  background-color: #F1EEE9;
  position: absolute;
  left: 30rem;
  bottom: 550px;
}
#get {
  position: absolute;
}
#overview {
  text-align: left;
  align-items: right;
  justify-content: right;
  gap: 1rem;
  overflow-wrap: break-word;
  margin-left: 43%;
  padding-top: 11.5em;
  float: right;  
}
#tagline {
  text-align: left;
  align-items: top;
  justify-content: left;
  float: left;
  color: #F1EEE9;
  margin-left: 1em;
  position: absolute;
  bottom: 445px;
  font-family: 'Quicksand', sans-serif;
  font-weight: lighter;
  font-size: 20px;
}
* {
  padding: 0px;
  margin: 0px;
}
#release_date {
  position: absolute;
  margin-top: 15em;
  display: inline-block;
  white-space: nowrap;
  margin-left: 1em;
  margin-bottom: -7.5em;
}
img {
  display: block;
  border-radius: 10px;
  margin-left: 1rem;
  position: absolute;
  margin-top: -15rem;
}
.Movies > img {
  position: absolute;
}
#title {
  font-size: 40px;
  position: absolute;
  top: 15rem;
  margin-left: 1rem;
  color: #F1EEE9;
  padding-bottom: 10px;
  text-transform: Uppercase;
}
v-for {
  display: flex;
  text-align: right;
  display: inline-flex;
  font-size: 15px;
  text-align: left;
  float: right;
  position: absolute;
  margin-top:26em;
  margin-left: 40%;
}
#revenue {
  font-size: 15px;
  position: relative;
  padding-top: 10%;
  padding-right: 38em;
}
#runtime {
  display:flex;
  position: absolute;
  margin-top: 15em;
  display: inline-block;
  margin-left: 26em;
  margin-bottom: -7.5em;
}
#vote_count, #vote_average, #popularity {
  display: inline;
  display: inline-block;
  align-content: right;
  justify-content: right;
  position: relative; top: 40px;
  line-height: 12px;
  white-space: nowrap;
  text-align: center;
  color:#F1EEE9;
}
#vote_count {
  padding: 5px;
  margin: 0px;
  background-color: #d38806;
  border-radius: 1em;
  border-spacing: 1em;
  position: relative; left: 550px;
}
#vote_average {
  padding: 5px;
  margin: 0px;
  background-color: #d38806;
  border-radius: 1em;
  border-spacing: 1em;
  position: relative; left: 570px;
}
#popularity {
  padding: 5px;
  margin: 0px;
  background-color: #d38806;
  border-radius: 1em;
  border-spacing: 1em;
  position: relative; left: 590px;
}
#release_date, #runtime {
  bottom: 540px;
} 
</style>
