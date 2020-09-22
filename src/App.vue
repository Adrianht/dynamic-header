<template>
  <div id="app" :class="isOpen ? 'tablet-nav-open' : ''">
    <Header @menuClicked="toggleShadow" />
    <Main />
    <Footer />
  </div>
</template>

<script>
import Header from "@/components/Header";
import Main from "@/components/Main";
import Footer from "@/components/Footer";

export default {
  name: "App",
  components: {
    Header,
    Main,
    Footer
  },
  data() {
    return {
      isOpen: false
    };
  },
  methods: {
    toggleShadow(isOpen) {
      this.isOpen = isOpen;
    }
  }
};
</script>

<style lang="scss">
@import "./styles/reset";

body {
  background-color: #fffaf4;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: grid;
  grid-template-rows: 60px 1fr auto;
  grid-template-columns: repeat(12, 1fr);
  height: 100vh;
  width: 100vw;

  &.tablet-nav-open {
    -webkit-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    height: 100%;
  }
}

header {
  grid-row: 1;
  grid-column: 1 / -1;
}

main {
  grid-row: 2;
  grid-column: 2 / -2;
  padding: 1em;
}

footer {
  grid-row: 3;
  grid-column: 1 / -1;
}
</style>
