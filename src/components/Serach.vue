<template>
  <div id="main-container">
    <div class="search-box">
      <h2>Nasa Api Project</h2>
      <form v-on:submit.prevent="getResult(query)">
        <input
          class="serch-input"
          type="text"
          placeholder="Type in your search"
          v-model="query"
        />
        <button class="myButton">Submit</button>
      </form>
      <div class="grid-container" v-if="results">
        <div
          class="sub-container"
          v-for="(result, index) in results"
          :key="index"
        >
          <img v-bind:src="result.links[0].href" />
        </div>
      </div>
      <footer class="footer">
        <p>
          Copyright <span class="copy-color">&copy;</span> Akram Sheikh 2021.
        </p>
      </footer>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      msg: "Search",
      query: "",
      results: "",
      show: false,
    };
  },
  mounted() {
    this.getResult("moon");
  },
  methods: {
    getResult(query) {
      axios
        .get(
          "https://images-api.nasa.gov/search?q=" + query + "&media_type=image"
        )
        .then((response) => {
          console.log(response.data.collection.items);
          this.results = response.data.collection.items;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,600;0,700;0,900;1,100;1,200;1,400;1,500;1,600;1,800&display=swap");
/* Reset */
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
/* Container */
#main-container {
  font-family: "Montserrat", sans-serif;
  background: rgb(7, 77, 60);
}

h2 {
  color: #fff;
  font-size: 4rem;
  padding: 1rem;
  margin-bottom: 2rem;
  text-shadow: 2px 2px 0 #bcbcbc, 4px 4px 0 #9c9c9c,
    -1px 8px 8px rgba(206, 89, 55, 0.02);
}

img {
  width: 100%;
  height: 100%;
  border-radius: 15px;
}

form {
  margin-bottom: 3rem;
}

/* Search Box */
.search-box {
  max-width: 1280px;
  margin: auto;
  text-align: center;
}

/* Serch Input */
.serch-input {
  font-size: 18px;
  width: 250px;
  margin-right: 1rem;
  padding: 15px 10px;
  border: none;
  border-radius: 4px 4px 4px 15px;
  outline: none;
  transition: 0.5s;
}
.serch-input::placeholder {
  color: gray;
}
.serch-input:focus {
  border: none;
  outline: none;
  color: #fff;
  background-color: #276873;
}

/* btn */
.myButton {
  box-shadow: 1px 2px 6px 0px #276873;
  background: linear-gradient(to bottom, #599bb3 5%, #408c99 100%);
  background-color: #599bb3;
  border-radius: 31px;
  border: 2px solid #29668f;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Courier New;
  font-size: 22px;
  font-weight: bold;
  padding: 14px 38px;
  text-decoration: none;
  text-shadow: 6px 3px 2px #3d768a;
}
.myButton:hover {
  background: linear-gradient(to bottom, #408c99 5%, #599bb3 100%);
  background-color: #408c99;
}
.myButton:active {
  position: relative;
  top: 1px;
}

/* Grid Container */
.grid-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}
.sub-container {
  border: 1px solid green;
  border-radius: 15px;
}

/* Footer Sections */
.footer {
  margin-top: 20px;
  background-color: #5598af;
}

.footer p {
  text-align: center;
  padding: 1rem;
}
.copy-color {
  color: red;
}

/*** Responsive Design ****/
@media (max-width: 768px) {
  .serch-input {
    margin-bottom: 2rem;
  }
  h2 {
    font-size: 3rem;
  }
  p {
    text-align: center;
  }

  .grid-container {
    display: grid;
    grid-template-columns: 1fr;
  }
  .sub-container img {
    width: 90%;
  }
}
</style>
