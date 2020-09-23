<template>
  <div id="app">
    <Header />
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
  }
};
</script>

<style lang="scss">
@import "./styles/reset";
@import "./styles/media-queries";

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
}

header {
  grid-row: 1;
  grid-column: 1 / -1;
}

main {
  grid-row: 2;
  grid-column: 2 / -2;
  padding: 1em;
  @include desktop {
    grid-column: 4 / -4;
  }
}

footer {
  grid-row: 3;
  grid-column: 1 / -1;
}
</style>
