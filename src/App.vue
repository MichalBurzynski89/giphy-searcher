<template>
  <div id="app">
    <SearchBar />
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
      error: null
    };
  },
  created() {
    fetch(`http://api.giphy.com/v1/gifs/trending?api_key=${API_KEY}`)
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
