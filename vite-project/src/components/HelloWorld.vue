<template>
  <div id="main">
    <div id="h1">
  <h1> Movies </h1>
  </div>
  <div id="label">
  <label for="Movies">Select Movies here:</label>
  </div>
    <div id="div1"></div>
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
  </div>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios"

const Movies = ref("");
const response = ref(null);

const getMovies = async () => {
console.log(Movies.value)
const movieData = await getData(`https://api.themoviedb.org/3/movie/${Movies.value}`, {
  params: {
    api_key: "354ab13223b58e3243b70a0085da1b2e",
  } 
});
  callMovies(movieData.data);

}
const getData = async (url, params) => {
  try {
    return await axios.get(url, params);
  } catch (error) {
    console.log(error)
  }
};

function callMovies(movieData) {
 document.getElementById('div1').innerHTML = "";

const runtime = document.createElement("p");
 runtime.innerHTML = 'Runtime: ' + movieData['runtime'];
 runtime.setAttribute('id', 'runtime');
 document.getElementById('div1').appendChild(runtime); 
 
const overview = document.createElement("p");
 overview.innerHTML = '<br>Overview</br>' + movieData['overview'];
 overview.setAttribute('id', 'overview');
 document.getElementById('div1').appendChild(overview);
  
const img = document.createElement("img");
 img.src = 'https://image.tmdb.org/t/p/w500' + movieData['poster_path'];
 img.setAttribute('id', 'img');
 document.getElementById('div1').appendChild(img);
  
const release_date = document.createElement("p");
 release_date.innerHTML = 'Release Date: ' + movieData['release_date'];
 release_date.setAttribute('id', 'release_date');
 document.getElementById('div1').appendChild(release_date);
  
const original_title = document.createElement("h1");
 original_title.innerHTML = movieData['original_title'];
 original_title.setAttribute('id', 'movietitle');
 document.getElementById('div1').appendChild(original_title);

let genres = genre(movieData['genres']);
console.log(genres);
const callgenres = document.createElement("p");
 callgenres.innerHTML = '<b><pre>Genres<pre/></b>'+ genres;
 callgenres.setAttribute('id', 'genres');
 document.getElementById('div1').appendChild(callgenres);

const revenue = document.createElement('p');
 revenue.innerHTML = '<pre><b>Revenue</b></pre>' + '$' + movieData['revenue'] + '  USD';
 revenue.setAttribute('id', 'revenue');
 document.getElementById('div1').appendChild(revenue);

const tagline = document.createElement('h2');
 tagline.innerHTML =  movieData['tagline'];
 tagline.setAttribute('id', 'tagline');
 document.getElementById('div1').appendChild(tagline);

const popularity = document.createElement('p');
 popularity.innerHTML = '<br>Popularity</br> ' +  movieData['popularity']; 
 popularity.setAttribute('id', 'popularity');
 document.getElementById('div1').appendChild(popularity);

const vote_average = document.createElement('p');
 vote_average.innerHTML = '<br>Vote Average</br> ' + movieData['vote_average']; 
 vote_average.setAttribute('id', 'vote_average');
 document.getElementById('div1').appendChild(vote_average);

const vote_count = document.createElement('p');
 vote_count.innerHTML = '<br>Vote Count</br> ' + movieData['vote_count']; 
 vote_count.setAttribute('id', 'vote_count');
 document.getElementById('div1').appendChild(vote_count);
};

function genre(genresArray) {
  let callgenres = ""
  for (i=0 ; i < genresArray.length; i++) {
    let genre = genres[genresArray[i].id]
    callgenres = callgenres + (genre + ', ')
  }
  let result = callgenres.slice(0, callgenres.length - 2) 
  return result
};



   const genres = {
    28: 'Action',
    12: 'Adventure',
    16: 'Animantion',
    35: 'Comedy',
    80: 'Crime',
    18: 'Drama',
    10751: 'Family',
    14: 'Fantasy',
    9648: 'Mystery',
    10749: 'Romance',
    53: 'Thriller',
    878: 'Science Fiction',
  };

</script>

<style scoped>
#main {
  background-color: #44276a;
  background-image: url(https://images.pexels.com/photos/7605490/pexels-photo-7605490.jpeg?auto=compress&cs=tinysrgb&dpr=3&h=750&w=1260);
  background-size: cover;
  background-repeat: no-repeat;
  max-width: 1280px;
  max-height: 1024px;
}

p {
  font-family: 'Montserrat', sans-serif;
  color: #F1EEE9;
  text-align: right;
}

#main > #h1 {
  color: #F1EEE9;
  font-family: 'Merriweather', serif;
  font-size: 100px;
  text-align: center;
  padding-left: 8rem;
  padding-bottom: 1rem;
}

#main > #label {
  display: flex;
  color: #F1EEE9;
  font-family: 'Merriweather', serif;
  font-size: 30px;
  text-align: center; 
  justify-content: center;
  position: relative;
  left: 35rem;
}

#main > #label, #get, #Movies {
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
  bottom: 530px;
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
  margin-left: 45%;
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
}



* {
  padding: 0px;
  margin: 0px;
}

#release_date {
  display:flex;
  position: absolute;
  margin-top: 15em;
  display: inline-block;
  white-space: nowrap;
  margin-left: 1em;
  margin-bottom: -7.5em; 
}

#img {
  border-radius: 10px;
  display:flex;
  margin-top: 12em;
  margin-left: 1rem;
  position: absolute;
}

#movietitle {
  font-size: 40px;
  position: absolute;
  top: 15rem;
  margin-left: 1rem;
  color: #F1EEE9;
  padding-bottom: 10px;
  text-transform: Uppercase;
}

#genres {
  display: flex;
  text-align: right;
  display: inline-flex;
  font-size: 15px;
  text-align: left;
  float: right;
  position: absolute;
  margin-top:26em;
  margin-left: 38.5%;


}

#revenue {
  font-size: 15px;
  position: relative;
  padding-top: 30.5%;
  padding-right: 1em;

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
  position: relative; left: 590px;

}

#vote_count:hover {
  background-color: gray;
}

#vote_average {
  padding: 5px;
  margin: 0px;
  background-color: #d38806;
  border-radius: 1em;
  border-spacing: 1em;
  position: relative; left: 580px;

}

#vote_average:hover {
  background-color: gray;
}

#popularity {
  padding: 5px;
  margin: 0px;
  background-color: #d38806;
  border-radius: 1em;
  border-spacing: 1em;
  position: relative; left: 570px;

}

#popularity:hover {
  background-color: gray;
}

#release_date, #runtime {
  bottom: 510px;
}
</style>
