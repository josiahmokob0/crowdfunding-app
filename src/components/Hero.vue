<template>
  <div class="header--bg">
    <div class="header container-xl">
      <a href="" class="header__logo">
        <img src="../assets/logo.svg" alt="crowdfunding - home">
      </a>
        <DesktopNav />
      <div class="header__hamburger">
        <Hamburger :open="open" />
      </div>
    </div>
    <div v-if="open" class="mobile-nav">
      <MobileNav />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

import MobileNav from './nav/Mobile.vue';
import DesktopNav from './nav/Desktop.vue';
import Hamburger from './reusable/Hamburger.vue';

export default {
  components: {
    MobileNav,
    Hamburger,
    DesktopNav,
  },
  computed: {
    open() {
      return this.openMenu();
    },
  },
  methods: {
    ...mapGetters(['openMenu']),
  },
};
</script>

<style lang="scss">
.mobile-nav, .header__hamburger {
  position: initial;
  @media (min-width: 50em) {
    opacity: 0;
    position: absolute;
    z-index: -1;
  }
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: var(--bg-spacer);

  &--bg {
    background: no-repeat center rgba(0, 0, 0, 0.15);
    background-size: cover;
    background-blend-mode: multiply;
    background-image: url(../assets/image-hero-mobile.jpg);
    min-height: 20rem;

    @media (min-width: 50em) {
      background-image: url(../assets/image-hero-desktop.jpg);
      min-height: 25rem;
    }
  }

  &__hamburger {
    cursor: pointer;
  }
}

.container-xl {
  max-width: var(--text-width);
  width: 80%;
  margin: 0 auto;

  @media (min-width: 50em) {
    max-width: 120em;
    width: 80%;
    margin: 0 auto;
  }
}
</style>
