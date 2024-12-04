<template>
  <header class="header" :class="{ 'header--scrolled': pageScrolled }">
    <Logo :color="logoColor" />
    <nav class="nav">
      <ThemeSwitch v-on:theme-change="updateLogo" />
      <button @click="toggleNavbar" class="menu-button">
        <transition name="theme">
          <MenuIcon v-if="logoColor === 'bright'" key="bright" class="menu" stroke="black" />
        </transition>
        <transition name="theme">
          <MenuIcon v-if="logoColor === 'dark'" key="dark" class="menu" stroke="white" />
        </transition>
      </button>
    </nav>
    <Navbar :isOpen="isNavbarOpen" @close="toggleNavbar(false)" />
  </header>
</template>

<script>
import ThemeSwitch from "~/components/ThemeSwitch.vue";
import Logo from "~/components/Logo.vue";
import Navbar from "~/components/Navbar.vue";
import { MenuIcon } from "vue-feather-icons";

export default {
  components: {
    ThemeSwitch,
    Logo,
    Navbar,
    MenuIcon,
  },
  data() {
    return {
      pageScrolled: false,
      logoColor: "bright", // Can be 'bright' or 'dark'
      isNavbarOpen: false,
    };
  },
  methods: {
    updateLogo() {
      this.logoColor = this.logoColor === "dark" ? "bright" : "dark";
    },
    toggleNavbar(state = null) {
      this.isNavbarOpen = state !== null ? state : !this.isNavbarOpen;
    },
    headerScroll() {
      const fromTop = window.scrollY;
      this.pageScrolled = fromTop > 40;
    },
  },
  mounted() {
    window.addEventListener("scroll", this.headerScroll);
    if (process.isClient) {
      this.logoColor = localStorage.getItem("theme");
    }
  },
};
</script>

<style lang="scss" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  padding: 15px 30px;
  transition: padding 0.15s linear, background 0.15s linear, border-color 0.15s linear;
  border-bottom: 1px solid transparent;
}

.nav {
  display: flex;
  align-items: center;
}

.menu-button {
  background: none;
  border: none;
  cursor: pointer;
}

.menu {
  width: 24px;
  height: 24px;
}

.theme-enter-active,
.theme-leave-active {
  transition: opacity 0.3s;
}

.theme-enter,
.theme-leave-to {
  opacity: 0;
}
</style>
