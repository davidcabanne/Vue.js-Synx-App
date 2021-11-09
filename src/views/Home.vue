<template>
  <Background />
  <Nav />
  <Hero />
  <Search
    :key="componentKey"
    @reload-search-component="reloadSearchComponent"
  />
  <Artists />
  <MainContainer />
  <MainSpacer />
</template>

<script>
// => Components
import Background from "@/components/Background";
import Nav from "@/components/Nav";
import Hero from "@/components/Hero";
import Search from "@/components/Search";
import Artists from "@/components/Artists";
import MainContainer from "@/components/MainContainer";
import MainSpacer from "@/components/MainSpacer";

export default {
  name: "Home",
  components: {
    Background,
    Nav,
    Hero,
    Search,
    Artists,
    MainContainer,
    MainSpacer,
  },
  data() {
    return {
      componentKey: 0,
    };
  },
  methods: {
    reloadSearchComponent: function() {
      this.componentKey += 1;
    },
  },
};
</script>

<style></style>
