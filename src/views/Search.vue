<template>
  <div :class="[{ [$style.flexStart]: step === 1 }, [$style.search]]">
    <Claim v-if="step === 0"/>
    <SearchInput
      :searchingValue="searchValue"
      v-model="searchValue"
      @input="handleInput"
      :dark="step === 1"
    />
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <transition name="slide">
      <img src="../assets/logo.svg" :class="[$style.logo]" v-if="step === 1">
    </transition>

    <div :class="[$style.results]" v-if="results && !loading && step === 1">
      <Item v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div :class="[$style.loader]" v-if="step === 1 && loading" />
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>


<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';
import HeroImage from '@/components/HeroImage.vue';
import SearchInput from '@/components/SearchInput.vue';
import Claim from '@/components/Claim.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim, SearchInput, HeroImage, Item, Modal,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`).then((respone) => {
        this.results = respone.data.collection.items;
        this.loading = false;
        this.step = 1;
      }).catch((err) => {
        throw err;
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

    &.flexStart {
      justify-content: flex-start;
    }

    .logo {
      position: absolute;
      top: 30px;
    }

    .results {
      margin-top: 50px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;
      @media (min-width: 768px) {
        width: 90%;
        grid-template-columns: 1fr 1fr 1fr;
      }
    }

    .loader {
      margin-top: 100px;
      display: inline-block;
      width: 64px;
      height: 64px;
      @media (min-width: 768px) {
        width: 90px;
        height: 90px;
      }
      &:after {
        content: " ";
        display: block;
        width: 46px;
        height: 46px;
        margin: 1px;
        border-radius: 50%;
        border: 5px solid #1e3d4a;
        border-color: #1e3d4a transparent #1e3d4a transparent;
        animation: loading 1.2s linear infinite;
        @media (min-width: 768px) {
          width: 90px;
          height: 90px;
        }
      }
    }

    @keyframes loading {
      0% {
        transform: rotate(0deg);
      }
      100% {
        transform: rotate(360deg);
      }
    }
  }


</style>

<style scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }
</style>
