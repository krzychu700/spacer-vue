<template>
  <div :class="$style['search']">
    <Claim />
    <SearchInput :searchingValue="searchValue" v-model="searchValue" @input="handleInput"/>
    <HeroImage />
  </div>
</template>


<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import HeroImage from '@/components/HeroImage.vue';
import SearchInput from '@/components/SearchInput.vue';
import Claim from '@/components/Claim.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: { Claim, SearchInput, HeroImage },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      console.log(this.searchValue);
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
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

</style>
