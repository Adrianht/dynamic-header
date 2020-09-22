<template>
  <header>
    <a href="#" id="my-icon">
      <img :src="champagne" alt="champagne!" />
    </a>
    <nav class="navbar" :class="{ 'navbar--hidden': !this.showNavbar }">
      <section class="route-container">
        <a href="#" class="route-link">Home</a>
        <a href="#" class="route-link">Projects</a>
        <a href="#" class="route-link">Customers</a>
        <a href="#" class="route-link">About us</a>
        <a href="#" class="route-link">Employees</a>
      </section>

      <a class="menu-toggle-container" aria-label="show-menu" @click="toggleMenu" :class="isOpen ? 'open' : 'collapsed'" >
        <span class="menu-toggle"></span>
        <span class="menu-toggle"></span>
        <span class="menu-toggle"></span>
      </a>

      <section class="mobile-navigation" :class="isOpen ? 'open' : 'collapsed'" >
        <div class="menu-item-link" >
          <a href="#" class="route-link">Home</a>
          <a href="#" class="route-link">Projects</a>
          <a href="#" class="route-link">Customers</a>
          <a href="#" class="route-link">About us</a>
          <a href="#" class="route-link">Employees</a>
        </div>
      </section>
      
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      champagne: require('../assets/champagne.svg'),
      showNavbar: true,
      lastScrollPos: 0,
      isOpen: false
    };
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll);
    const el = document.getElementById("my-icon");
    console.log(el);
    el.addEventListener("mouseover", this.iconIsHovered);
  },
  methods: {
    onScroll() {
      const currentScrollPos =
        window.pageYOffset || document.documentElement.scrollTop;
      if (currentScrollPos < 0) {
        return;
      }

      if (Math.abs(currentScrollPos - this.lastScrollPos) < 60) {
        return;
      }

      this.showNavbar = currentScrollPos < this.lastScrollPos;
      this.lastScrollPos = currentScrollPos;
    },
    iconIsHovered() {
      this.showNavbar = true;
    },
    toggleMenu(){
      this.isOpen = this.isOpen ? false : true;
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/media-queries.scss";

nav {
  background-color: #aebab1;
  width: 100%;
  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: repeat(6, 1fr);
}

.navbar {
  height: 5em;
  width: 100vw;
}

.route-link {
  text-decoration: none;
  color: #2d1e1e;
  &:hover {
    text-underline-position: under;
    text-decoration: underline 2px solid pink;
  }
}

@include mobile {

  .route-container {
    display: none;
  }

  .menu-toggle-container {
    position: fixed;
    justify-self: right;
    margin-right: 1em;
    align-self: center;
    color: #1e1e1e;
    border-radius: 50% 50%;
    z-index: 3;
    width: 42px;
    height: 42px;
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    
    &:hover {
      cursor: pointer;
    }

    span {
      display: block;
      position: relative;
      border-radius: 3px;
      height: 3px;
      width: 18px;
      background: #111;
      z-index: 1;
      transform-origin: 4px 0px;
      transition: 
        transform 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
        background 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
        opacity 0.55s ease;
    }
    
    span:first-child {
      transform-origin: 0% 0%;
      margin-bottom: 4px;
    }

    span:nth-last-child(2) {
      transform-origin: 0% 100%;
      margin-bottom: 4px;
    }

    &.open {
      span {
        opacity: 1;
        transform: rotate(-45deg) translate(2px, -2px);
        background: #232323;
      }

      span:nth-last-child(2) {
        opacity: 0;
        transform: rotate(0deg) scale(0.2, 0.2);
      }

      span:nth-last-child(3) {
        transform: rotate(45deg) translate(3.5px, -2px);
      }
    }

    &.open {
      background: #fff;
    }
  }

  #my-icon {
    position: absolute;
    margin: 1em 0 0 2em;
    z-index: 2;
    height: 3em;
    width: 3em;
  }



  .mobile-navigation {
    position: fixed;
    top: 0;
    background-color: #aebab1;
    width: 100%;
    z-index: 2;
    overflow: hidden;
    transition: max-height 0.5s ease-out;
    height: 100vh;
    max-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    row-gap: 3em;

    &.collapsed{
      max-height: 0%;
    }

    a{
      text-decoration: none;
    }

    .route-link {
      font-size: 3em;
      outline: 0;
      text-decoration: none;
      color: #1e1e1e;
      border-bottom: 4px solid transparent;
      display: block;

      &.open{
        -webkit-animation: fadeInFromNone 3s ease-out;
        -moz-animation: fadeInFromNone 3s ease-out;
        -o-animation: fadeInFromNone 3s ease-out;
        animation: fadeInFromNone 3s ease-out;
      }

      &:hover{
        cursor: pointer;
        border-color: pink;
      }
    }
  }

  @-webkit-keyframes fadeInFromNone {
    0% {
        display: none;
        opacity: 0;
    }

    10% {
        display: block;
        opacity: 0;
    }

    100% {
        display: block;
        opacity: 1;
    }
  }

  @-moz-keyframes fadeInFromNone {
    0% {
        display: none;
        opacity: 0;
    }

    10% {
        display: block;
        opacity: 0;
    }

    100% {
        display: block;
        opacity: 1;
    }
  }

  @-o-keyframes fadeInFromNone {
    0% {
        display: none;
        opacity: 0;
    }

    10% {
        display: block;
        opacity: 0;
    }

    100% {
        display: block;
        opacity: 1;
    }
  }

  @keyframes fadeInFromNone {
    0% {
        display: none;
        opacity: 0;
    }

    10% {
        display: block;
        opacity: 0;
    }

    100% {
        display: block;
        opacity: 1;
    }
  }

}


@include tablet {
  .menu-toggle-container {
    display: none;
  }
  nav {
    display: grid;
    grid-template-columns: 10em 1fr;
    align-items: center;

    .route-container {
      grid-column: 2 / -1;
      width: 100%;
      display: grid;
      grid: 1fr / auto-flow max-content;
      justify-content: space-evenly;
      margin: 0 auto;
    }
  }

  .navbar {
    height: 5em;
    width: 100vw;
    position: fixed;
    box-shadow: 0 2px 15px rgba(71, 120, 120, 0.5);
    transform: translate3d(0, 0, 0);
    transition: height 0.5s linear, top 0.5s ease-in-out 0s;
    transform-origin: 50% 0;

    &.navbar--hidden {
      box-shadow: none;
      transform: translate3d(0, -100%, 0);
    }
  }


  #my-icon {
    position: fixed;
    margin: 0.5rem 0 0 2rem;
    z-index: 2;
    height: 4em;
    width: 4em;
  }
}

</style>
