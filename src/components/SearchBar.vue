<template>
  <div class="wrapper">
    <h1 class="title">Giphy Searcher</h1>
    <form class="search-form">
      <input type="search" placeholder="Enter a word or phrase..." class="search-form__input" id="searchInput">
      <button type="submit" class="search-form__button">Search</button>
    </form> 
  </div>
</template>

<script>
export default {
  name: "SearchBar"
};
</script>

<style lang="less" scoped>
.wrapper {
  text-align: center;
  padding: 0 8px;

  .title {
    color: #fff;
    font-weight: 800;
    font-size: 36px;
    text-shadow: 4px 4px 16px #222;

    @media (min-width: 768px) {
      font-size: 48px;
    }

    @media (min-width: 1024px) {
      font-size: 56px;
    }
  }
}

.search-form {
  display: flex;
  justify-content: center;

  .search-form__input {
    padding: 6px 10px;
    flex-grow: 1;
    max-width: 70%;
    font-size: 16px;
    border: 2px solid goldenrod;
    border-top-left-radius: 4px;
    border-bottom-left-radius: 4px;
    background-color: aqua;
    color: darkolivegreen;

    &:focus {
      outline: none;
    }

    @media (min-width: 768px) {
      padding: 8px 16px;
    }

    @media (min-width: 1024px) {
      max-width: 700px;
      padding: 12px 16px;
      font-size: 20px;
      border-width: 3px;
    }
  }

  .search-form__button {
    font-size: 16px;
    background-color: goldenrod;
    border: none;
    color: #fff;
    font-weight: 600;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    cursor: pointer;
    transition: background-color 0.25s ease-in-out;

    &:hover {
      background-color: darken(goldenrod, 10%);
    }

    @media (min-width: 1024px) {
      font-size: 20px;
      padding: 0 16px;
    }
  }
}
</style>
