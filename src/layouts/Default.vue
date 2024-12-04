<template>
  <div class="site">
    <Header :menuToggle="sidebar" />
    <Sidebar v-if="sidebar" />
    <main class="main" :class="{
      'main--no-sidebar': !sidebar,
      'main--sidebar-is-open': this.$store.state.sidebarOpen,}">
      <slot />
    </main>
  </div>
</template>

<script>
import Header from "~/components/Header.vue";
import Sidebar from "~/components/Sidebar.vue";
import CookieMonster from "~/components/CookieMonster.vue"; // Import CookieMonster
import SiteFooter from "~/components/Footer.vue"; // Import Footer

export default {
  components: {
    Header,
    Sidebar,
    CookieMonster, // Register CookieMonster
    SiteFooter, // Register Footer
  },
  props: {
    sidebar: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      showCookieMonster: true, // Show CookieMonster by default
    };
  },
  methods: {
    hideCookieMonster() {
      // Hide the CookieMonster and show the footer
      this.showCookieMonster = false;
    },
  },
  mounted() {
    this.$store.commit("closeSidebar");
    if (process.isClient) {
      if ("serviceWorker" in navigator) {
        navigator.serviceWorker
          .register("/sw.js")
          .then(() => {
            console.log("Service Worker Registered");
          });
      }
    }
  },
};
</script>

<style lang="scss" scoped>
.site {
  overflow: hidden;
}

.main {
  padding: 100px 30px 30px 30px;
  max-width: 800px;
  margin-bottom: 80px;
  /* Adds space between main content and footer */
  transition: transform 0.15s ease-in-out;

  @include respond-above(sm) {
    padding: 100px 30px 30px;
    transform: translateX(300px);
    width: calc(100% - 300px);
  }

  @include respond-above(md) {
    padding: 100px 80px 30px;
  }

  &--no-sidebar {
    transform: translate(0);
    margin: 0 auto;
    width: 100%;
    max-width: 1400px;
  }

  &--sidebar-is-open {
    transform: translate(300px);
  }
}

footer.site-footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #2a2a2a;
  color: rgba(255, 255, 255, 0.9);
  text-align: center;
  box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.2);
  z-index: 10;
  padding: 1rem;
}


</style>
