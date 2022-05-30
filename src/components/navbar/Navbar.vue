<template lang="html">
  <header class="s-navbar" id="navbar" :class="{'scrolled-nav':scrollNavbar}">
    <nav class="s-navbar-container">
      <div class="s-navbar-branding">
        <slot name="branding">
          <p style="margin: 0">
            Suhaib
          </p>
          <p style="margin: 0">
            Development
          </p>
        </slot>
      </div>
      <slot>
        <ul class="s-navbar-list" v-show="!mobile">
          <li class="s-navbar-item">
            <router-link to="/" class="s-navbar-link">
              Home
            </router-link>
          </li>
          <li class="s-navbar-item">
            <router-link to="/about" class="s-navbar-link">
              About
            </router-link>
          </li>
          <li class="s-navbar-item">
            <router-link to="/sushs" class="s-navbar-link">
              Contact us
            </router-link>
          </li>
        </ul>
      </slot>
      <slot name="burger-menu">
        <div class="s-navbar-button" v-show="mobile">
          <transition name="s-navbar-animation">
            <img v-if="!menuActive" @click="menuActive =! menuActive" src="@/assets/icons/menu.svg" alt="menu"
                 width="40" height="40" class="s-navbar-burger">
            <img class="s-navbar-burger" v-else src="@/assets/icons/close.svg" @click="menuActive =! menuActive"
                 alt="menu" width="40"
                 height="40">
          </transition>
        </div>
      </slot>
    </nav>
    <transition name="animation">
      <ul class="s-navbar-sidebar" v-show="menuActive">
        <li class="s-navbar-item">
          <router-link to="/" class="s-navbar-link">
            Home
          </router-link>
        </li>
        <li class="s-navbar-item">
          <router-link to="/" class="s-navbar-link">
            Home
          </router-link>
        </li>
        <li class="s-navbar-item">
          <router-link to="/" class="s-navbar-link">
            Home
          </router-link>
        </li>
        <li class="s-navbar-item">
          <router-link to="/" class="s-navbar-link">
            Home
          </router-link>
        </li>
      </ul>
    </transition>
  </header>
</template>

<script>
export default {
  name: "s-navbar",
  data() {
    return {
      scrollNavbar: null,
      mobile: true,
      menuActive: true,
      windowWidth: null
    }
  },
  methods: {
    checkScreenSize() {
      this.windowWidth = window.innerWidth
      if (this.windowWidth > 750) {
        this.mobile = false;
        this.menuActive = false
        return;
      }
      this.mobile = true
    },
    checkScroll() {
      if (window.scrollY > 50) {
        this.scrollNavbar = true;
        return;
      }
      this.scrollNavbar = false;
    }
  },
  created() {
    window.addEventListener('resize', this.checkScreenSize)
  },
  mounted() {
    window.addEventListener('scroll', this.checkScroll)
  }
}
</script>


<style lang="scss" scoped>
$primary: #42b983;
$primary2: #2c3e50;
$white: #fff;

.s {
  padding: 0;
  margin: 0;

  &-navbar {
    background-color: $primary;
    width: 100%;
    z-index: 10;
    position: fixed;
    color: $white;
    transition: .5s ease all;

    &-container {
      display: flex;
      flex-direction: row;
      max-width: 1320px;
      margin: 0 auto;
      @media screen and (max-width: 768px) {
        width: 100%;
        max-width: 100%;
        padding: 0 15px;
      }
    }

    &-list {
      padding: 0;
      list-style: none;
      display: flex;
      flex: 1;
      align-items: center;
      justify-content: flex-end;
      gap: 20px;
      max-width: -webkit-fill-available;
    }

    &-branding {
      display: flex;
      justify-content: center;
      align-items: flex-start;
      flex-direction: column;
      font-weight: 700;
    }

    &-item, &-link {
      font-weight: 500;
      color: $white;
      border-bottom: 1.6px solid transparent;
      text-decoration: none;
      transition: all .5s ease;
    }

    &-item{
      padding: 10px 20px;
      @media screen and (max-width: 750px) {
        width: -webkit-fill-available;
      }
    }

    &-link{
      text-align: start;
      display: block;
      &:hover {
        color: $primary2;
        border-color: $primary2;
      }
    }

    &-burger {
      position: absolute;
      top: 3px;
      right: 15px;
    }

    &-sidebar {
      display: flex;
      flex-direction: column;
      flex: 1;
      align-items: flex-start;
      justify-content: flex-start;
      list-style: none;
      position: fixed;
      top: 0;
      padding: 40px 15px;
      margin: 0;
      height: 100%;
      min-width: 250px;
      max-width: 250px;
      left: 0;
      background-color: $primary;
      z-index: 100;
    }

  }
}

.animation-enter-active,
.animation-leave-active {
  transition: 1s ease all;
}

.animation-enter-from,
.animation-leave-to {
  transform: translateX(-270px);
}

.animation-enter-to {
  transform: translateX(0);
}



.s-navbar-animation-enter-active,
.s-navbar-animation-leave-active {
  transition: 1s ease all;
}

.s-navbar-animation-enter-from,
.s-navbar-animation-leave-to {
  transform: rotate(180deg);
  opacity: .1;
}

.s-navbar-animation-enter-to {
  opacity: 0;
  transform: rotate(0deg);

}
</style>
