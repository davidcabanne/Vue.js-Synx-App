<template :key="componentKey">
  <div class="bloc__container flex__ctr bloc__marginLrg">
    <div class="bloc__wrapper flex__ctr flex__col">
      <div class="search__ctaContainer flex__ctr">
        <div>Artist</div>
        <input
          class="search__ctaBtn"
          type="checkbox"
          id="switch"
          v-model="toggleSwitch"
          @click="toggleFunction()"
        /><label for="switch">Toggle</label>
        <div>Track</div>
        <span class="search__cta--spacer"></span>
        <div @click="toggleReset()" class="search__cta--reset">Reset</div>
      </div>
      <input
        class="form-row__input bloc__marginSml"
        type="text"
        :placeholder="'Search by ' + [[searchData]]"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      toggleSwitch: false,
      searchData: "",
    };
  },
  methods: {
    toggleFunction: function() {
      if (this.toggleSwitch) {
        this.searchData = "Artist";
      } else {
        this.searchData = "Track";
      }
      this.toggleFunction();
    },
    toggleReset() {
      this.$emit("reload-search-component");
    },
  },
  mounted() {
    this.searchData = "Artist";
  },
};
</script>

<style scoped>
.search__ctaContainer {
  width: 90vw;
  max-width: 1240px;
  justify-content: flex-end;
}

.search__ctaContainer > * {
  margin-right: var(--spaceSml);
}

.search__ctaBtn {
  margin-right: 0;
}

.search__cta--spacer {
  width: 2px;
  height: 12px;
  border-radius: 2px;
  opacity: 0.5;
  background: var(--light);
}

.search__cta--reset {
  cursor: pointer;
}

/* CTA Section */
input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  cursor: pointer;
  text-indent: -9999px;
  width: 30px;
  height: 15px;
  background: var(--MedGrey);
  display: block;
  border-radius: 100px;
  position: relative;
}

label:after {
  content: "";
  position: absolute;
  top: 0px;
  left: 0px;
  width: 15px;
  height: 15px;
  background: var(--light);
  border-radius: 30px;
  transition: 0.3s;
}

input:checked + label {
  background: var(--greenPrimary);
}

input:checked + label:after {
  left: calc(100%);
  transform: translateX(-100%);
}

label:active:after {
  width: 15px;
}

.form-row__input {
  padding: var(--spaceSml);
  width: 90vw;
  min-width: 100px;
  max-width: 1240px;
  color: var(--light);
  font-size: var(--body-firstFont);
  font-weight: 500;
  border-radius: 8px;
  border: 2px solid transparent;
  background: rgb(239, 239, 243, 0.1);
}

.form-row__input::placeholder {
  color: var(--MedGrey);
}

.form-row__input:focus {
  color: var(--MedGrey);
  color: var(--light);
}
</style>
