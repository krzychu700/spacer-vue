<template>
  <div :class="$style['search']">
    <div :class="$style['inputContainer']">
      <label for="search">Search</label>
      <input
        name="search"
        id="search"
        :class="$style['inputContainer__input']"
        v-model="searchValue"
        @input="handleInput"
      />
      <ul>
        <li v-for="item in results" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description}} </p>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`).then((respone) => {
        this.results = respone.data.collection.items;
      }).catch((err) => {
        console.log(err);
      });
    }, 500),
  },
};
</script>


<style module lang="scss">
  .search {
    margin: 0;
    padding: 30px;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;

    .inputContainer {
      display: flex;
      flex-direction: column;
      width: 300px;
      font-family: Montserrat, sans-serif;

      .inputContainer__input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
      }
    }
  }

</style>
