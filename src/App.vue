<template>
  <div id="app">
    <SearchBar v-bind:onSubmit="handleSubmit" v-bind:onInput="handleInput" v-bind:value="searchValue" />
    <div v-if="items.length" class="collection">
      <div v-for="item in items" v-bind:key="item.id" class="collection__item">
        <a v-bind:href="item.url" target="_blank" class="collection__link">
          <img
            v-bind:src="item.imageURL" 
            v-bind:alt="item.title" 
            v-bind:title="item.url"
            class="collection__img"
          >
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";

const API_KEY = "IxpCK9RNmcJYyK32CSBWHwthYUJStCO2";

export default {
  name: "App",
  components: {
    SearchBar
  },
  data() {
    return {
      items: [],
      isLoaded: false,
      error: null,
      searchValue: ""
    };
  },
  methods: {
    handleSubmit() {
      if (!this.searchValue) return;
      fetch(
        `http://api.giphy.com/v1/gifs/search?q=${
          this.searchValue
        }&api_key=${API_KEY}&limit=100`
      )
        .then(res => {
          if (res.ok) {
            return res.json();
          } else {
            throw new Error(
              `The connection ended with status ${res.status}${
                res.statusText ? ": " + res.statusText : ""
              }`
            );
          }
        })
        .then(json => {
          this.items = [];
          json.data.forEach(item => {
            const gif = {
              id: item.id,
              title: item.title,
              url: item.url,
              imageURL: item.images.original.url
            };
            this.items.push(gif);
          });
          console.log(this.items);
        })
        .catch(error => {
          this.error = error;
          alert(error);
        });
      this.searchValue = "";
      document.getElementById("searchInput").focus();
    },
    handleInput(e) {
      this.searchValue = e.target.value;
    }
  },
  created() {
    fetch(`http://api.giphy.com/v1/gifs/trending?api_key=${API_KEY}&limit=80`)
      .then(res => {
        if (res.ok) {
          this.isLoaded = true;
          return res.json();
        } else {
          throw new Error(
            `The connection ended with status ${res.status}${
              res.statusText ? ": " + res.statusText : ""
            }`
          );
        }
      })
      .then(json => {
        json.data.forEach(item => {
          const gif = {
            id: item.id,
            title: item.title,
            url: item.url,
            imageURL: item.images.original.url
          };
          this.items.push(gif);
        });
        console.log(this.items);
      })
      .catch(error => {
        this.isLoaded = true;
        this.error = error;
        alert(error);
      });
  }
};
</script>

<style lang="less">
* {
  box-sizing: border-box;
  list-style-type: none;
}

body {
  margin: 0;
  padding: 0;
  background-color: royalblue;
  min-width: 320px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;

  .collection {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    margin: 32px 0;

    @media (min-width: 1600px) {
      margin: 64px 0;
    }

    .collection__item {
      width: 320px;
      height: 320px;
      border: 2px solid goldenrod;

      .collection__img {
        display: block;
        width: 100%;
        height: 100%;
      }
    }
  }
}
</style>
