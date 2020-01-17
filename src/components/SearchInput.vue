<template>
  <div :class="[$style.inputContainer]">
    <input
      id="search"
      name="search"
      :class="{ [[$style.inputContainer__input,
                  $style.inputContainer__input__white].join(' ')]: !dark,
                [[$style.inputContainer__input,
                  $style.inputContainer__input__dark].join(' ')]: dark}"
      :searchingValue="value"
      @input="handleChange"
    />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    searchingValue: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style module lang="scss">
    .inputContainer {
      display: flex;
      flex-direction: column;
      width: 300px;
      font-family: Montserrat, sans-serif;

      .inputContainer__input {
        margin-top: 50px;
        display: flex;
        width: 250px;
        text-align: center;
        font-size: 18px;
        font-weight: 300;
        height: 30px;
        border: 0;
        background: none;
        transition: box-shadow .3s ease-out;

        @media (min-width: 1024px) {
          font-weight: 400;
        }
      }

      .inputContainer__input__white {
        color: white;
        border-bottom: 1px solid white;

        &:focus {
          outline: none;
          box-shadow: 0 10px 20px -8px rgba(255,255,255, .5);
        }
      }

      .inputContainer__input__dark {
        color: #1e3d4a;
        border-bottom: 1px solid #1e3d4a;

        &:focus {
          box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
        }
      }
    }


</style>
