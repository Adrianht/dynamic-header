<template>
  <header>
    <a
      href="#"
      id="my-icon"
      aria-hidden="true"
      :style="champagne"
      :class="{ 'is-not-scrolled': !this.isScrolledDown }"
    ></a>

    <div
      class="click-outside"
      :class="isOpen ? 'show' : 'collapsed'"
      @click="toggleMenu"
    ></div>

    <nav
      class="navbar"
      :class="{
        'navbar--hidden': !this.showNavbar,
        'is-scrolling': this.isScrolledDown,
        'menu-clicked': this.isOpen
      }"
    >
      <ul class="route-container">
        <li>
          <a href="#" class="route-link">Home</a>
        </li>
        <li>
          <a href="#" class="route-link">Projects</a>
        </li>
        <li>
          <a href="#" class="route-link">Customers</a>
        </li>
        <li>
          <a href="#" class="route-link">About us</a>
        </li>
        <li>
          <a href="#" class="route-link">Employees</a>
        </li>
      </ul>

      <a
        class="menu-toggle-container"
        aria-hidden="true"
        @click="toggleMenu"
        :class="isOpen ? 'open' : 'collapsed'"
      >
        <span class="menu-toggle"></span>
        <span class="menu-toggle"></span>
        <span class="menu-toggle"></span>
      </a>

      <section class="mobile-navigation" :class="isOpen ? 'open' : 'collapsed'">
        <ul class="menu-item-link">
          <li>
            <a href="#" class="route-link" @click="toggleMenu"> Home</a>
          </li>
          <li>
            <a href="#" class="route-link" @click="toggleMenu"> Projects</a>
          </li>
          <li>
            <a href="#" class="route-link" @click="toggleMenu"> Customers</a>
          </li>
          <li>
            <a href="#" class="route-link" @click="toggleMenu"> About us</a>
          </li>
          <li>
            <a href="#" class="route-link" @click="toggleMenu"> Employees</a>
          </li>
        </ul>
      </section>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      champagne: {
        backgroundImage: `url(${require("../assets/champagne.svg")})`
      },
      showNavbar: true,
      lastScrollPos: 0,
      isOpen: false,
      isScrolledDown: false
    };
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll);
    const el = document.getElementById("my-icon");
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
      this.isScrolledDown = currentScrollPos > 50;
      this.lastScrollPos = currentScrollPos;
    },
    iconIsHovered() {
      this.showNavbar = true;
    },
    toggleMenu() {
      let open = this.isOpen ? false : true;
      this.isOpen = open;
      if (open) {
        document.documentElement.style.overflow = "hidden";
      } else {
        document.documentElement.style.overflow = "auto";
      }
      this.$emit("menuClicked", open);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../styles/media-queries.scss";
@import "../styles/keyframes.scss";

#my-icon {
  position: fixed;
  height: 3em;
  width: 3em;
  z-index: 3;
  margin: 1em 0 0 1em;

  &.is-not-scrolled {
    -webkit-animation: rotateAndResize 0.5s ease-in;
    -moz-animation: rotateAndResize 0.5s ease-in;
    -o-animation: rotateAndResize 0.5s ease-in;
    animation: rotateAndResize 0.5s ease-in;
    animation-fill-mode: forwards;
  }
}

.click-outside {
  &.show {
    position: fixed;
    z-index: 2;
    width: 100vw;
    height: 100vh;
    -webkit-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
  }

  &.collapsed {
    display: none;
  }
}

.navbar {
  height: 5em;
  width: 100vw;
  background-color: #fffaf4;
  width: 100%;
  display: grid;
  grid-template-rows: 1fr;
  grid-template-columns: repeat(6, 1fr);
  position: relative;
  z-index: 2;

  &.menu-clicked {
    -webkit-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
    box-shadow: inset 100vw 0px 5px 0px rgba(0, 0, 0, 0.75);
  }

  &.is-scrolling {
    background-color: #aebab1;
    position: fixed;
    -webkit-animation: fadeInFromNone 0.5s ease-in;
    -moz-animation: fadeInFromNone 0.5s ease-in;
    -o-animation: fadeInFromNone 0.5s ease-in;
    animation: fadeInFromNone 0.5s ease-in;
  }
}

.route-link {
  text-decoration: none;
  color: #2d1e1e;
  &:hover {
    text-underline-position: under;
    text-decoration: underline 2px solid pink;
  }
}

.menu-toggle-container {
  position: fixed;
  right: 0;
  margin-top: 1em;
  margin-right: 1em;
  color: #1e1e1e;
  border-radius: 50% 50%;
  z-index: 3;
  width: 42px;
  height: 42px;
  background: #fffaf4;
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
    z-index: 3;
    transform-origin: 4px 0px;
    transition: transform 0.5s cubic-bezier(0.77, 0.2, 0.05, 1),
      background 0.5s cubic-bezier(0.77, 0.2, 0.05, 1), opacity 0.55s ease;
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
    background: #fff;
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
}

.mobile-navigation {
  position: fixed;
  background-color: #aebab1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 2;
  overflow: hidden;

  &.collapsed {
    max-height: 0%;
  }

  a {
    text-decoration: none;
  }

  .route-link {
    font-size: 3em;
    outline: 0;
    text-decoration: none;
    color: #1e1e1e;
    border-bottom: 4px solid transparent;
    display: block;

    &.open {
      -webkit-animation: fadeInFromNone 3s ease-out;
      -moz-animation: fadeInFromNone 3s ease-out;
      -o-animation: fadeInFromNone 3s ease-out;
      animation: fadeInFromNone 3s ease-out;
    }

    &:hover {
      cursor: pointer;
      border-color: pink;
    }
  }
}

@include mobile {
  .route-container {
    display: none;
  }

  .mobile-navigation {
    top: 0;
    width: 100%;
    height: 100vh;
    max-height: 100vh;
    transition: max-height 0.5s ease-out;
  }
}

@include tablet {
  .route-container {
    display: none;
  }

  .mobile-navigation {
    right: 0;
    width: 50vw;
    max-width: 50vw;
    height: 100%;
    transition: max-width 0.5s ease-out;

    &.collapsed {
      max-width: 0%;
    }
  }
}

@include desktop {
  .menu-toggle-container {
    display: none;
  }

  .mobile-navigation {
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

    &.navbar--hidden {
      box-shadow: none;
      transform: translate3d(0, -100%, 0);
    }

    &:not(.is-scrolling) {
      box-shadow: none;
    }
  }
}
</style>
