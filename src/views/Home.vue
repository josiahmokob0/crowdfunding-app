<template>
  <main>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Commissioner:wght@400;500;700&display=swap" rel="stylesheet">
    <div :class="{'overlay': show}" />
    <hero />
    <intro />
    <stats />
    <project />
    <reward />
    <success />
  </main>
</template>

<script>
import { mapGetters } from 'vuex';

import hero from '@/components/Hero.vue';
import intro from '@/components/Intro.vue';
import stats from '../components/Stats.vue';
import project from '../components/Project.vue';
import reward from '../components/RewardModal.vue';
import success from '../components/reusable/SuccessModal.vue';

import '../css/index.css';

export default {
  components: {
    hero,
    intro,
    stats,
    project,
    reward,
    success,
  },
  computed: {
    show() {
      return (
        this.showRewardModal()
        || this.openMenu()
        || this.showSuccessModal()
      );
    },
  },
  methods: {
    ...mapGetters(['showRewardModal', 'openMenu', 'showSuccessModal']),
  },
};
</script>

<style lang="scss">

body {
  --moderate-cyan: hsl(176, 50%, 47%);
  --dark-cyan: hsl(176, 72%, 28%);
  --black: hsl(0, 0%, 0%);
  --dark-gray: hsl(0, 0%, 48%);
  --white: hsl(0, 100%, 100%);
  --gray: hsl(0, 0%, 90%);
  --light-cyan: hsl(192, 29%, 97%);
  --bg-gray: hsl(0, 0%, 98%);

  --ff-default: 'Commissioner', sans-serif;
  --fs-base: 0.9375rem;
  --fs-h4: 1.2rem;
  --fs-h3: 1.5rem;

  --sm-spacer: 1rem;
  --bg-spacer: 2.5rem;

  --border-radius: 0.5rem;
  --text-width: 75ch;
  @media (min-width: 50em) {
    --fs-base: 1.1rem;
    --fs-h4: 1.5rem;
    --fs-h3: 2rem;

    --sm-spacer: 1.5rem;
    --bg-spacer: 3rem;
  }
  background-color: var(--bg-gray);
}

  main {
    font-family: var(--ff-default);
    font-size: var(--fs-base);
    color: var(--dark-gray);
    text-align: center;
    min-height: 100vh;
  }

  .overlay {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 5;
  }
</style>
