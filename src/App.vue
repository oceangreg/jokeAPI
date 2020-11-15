<template>
  <div id="app">
    <div class="container">
      <h1>JokeAPI - VUEJS</h1>
      <p>
        JokeAPI is a RESTful API that serves uniformly and well formatted jokes.
      </p>
      <button type="button" id="get-joke" @click="fetchAPIData">
        Press for a joke!
      </button>
      <div id="jokeContainer" v-if="responseAvailable == true">
        <p v-if="result.setup">
          <span><i class="fas fa-question-circle"></i>{{ result.setup }}</span>
          <span
            ><strong
              ><i class="far fa-laugh-squint"></i>{{ result.delivery }}</strong
            ></span
          >
        </p>
        <p else v-if="result.joke">
          <span><i class="fas fa-laugh-wink"></i>{{ result.joke }}</span>
        </p>
      </div>
    </div>
    <div class="credit">
      <span>(c) Gregory Clayton Development</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      response: "",
      result: this.response,
      responseAvailable: false,
      apiKey: "53ce98cebamsha6eac270a4929a1p1882e4jsnef235d280449",
    };
  },

  methods: {
    fetchAPIData() {
      this.responseAvailable = false;
      fetch("https://sv443.net/jokeapi/v2/joke/Programming", {
        method: "GET",
      })
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            alert(
              "Server returned " + response.status + " : " + response.statusText
            );
          }
        })
        .then((response) => {
          this.result = response;
          this.responseAvailable = true;
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
body {
  background-image: linear-gradient(120deg, #f093fb 0%, #f5576c 100%);
  margin: 0px;
  height: 95vh;
}

h1 {
  font-size: 60px;
  color: white;
  text-shadow: 4px 4px 1px #f45e9f;
  letter-spacing: 1.5px;
  font-family: "Roboto", sans-serif;
  font-weight: bolder;
  margin-bottom: 0px;
}

p {
  color: white;
  font-family: "Roboto", sans-serif;
  font-size: 18px;
  margin-bottom: 0px;
}

.container {
  max-width: 600px;
  margin: auto;
}

#get-joke {
  display: block;
  margin: 30px 20px 30px 0px;
  padding: 15px 30px;
  border-radius: 100px;
  color: white;
  font-size: 20px;
  text-transform: uppercase;
  cursor: pointer;
  background: #f55e7c;
  font-family: "Roboto", sans-serif;
  font-weight: bolder;
  border: 2px solid #f9d6e1;
}

#jokeContainer {
  background: #ffffff1a;
  padding: 30px;
  margin-top: 20px;
}

#jokeContainer span {
  display: block;
  line-height: 26px;
  text-align: justify;
}

#jokeContainer p {
  margin-top: 0;
}

strong {
  margin-top: 5px;
  display: block;
}

i {
  color: #f4f4aa;
  background: black;
  padding: 6px;
  border-radius: 100px;
  margin-right: 10px;
}

.credit {
  position: absolute;
  bottom: 0;
  background: #ffffff26;
  width: 100%;
  text-align: center;
  padding: 10px 0px;
  color: white;
  font-family: "Roboto", sans-serif;
  font-size: 18px;
}
</style>
