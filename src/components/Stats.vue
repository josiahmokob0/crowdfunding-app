<template>
  <div class="stats container">

    <div class="stat">
      <h3 class="stat__title">${{backed}}</h3>
      <p class="stat__text">of ${{target}} backed</p>
    </div>

    <div class="stat">
      <h3 class="stat__title">{{backers}}</h3>
      <p class="stat__text">total backers</p>
    </div>

    <div class="stat">
      <h3 class="stat__title">{{daysLeft}}</h3>
      <p class="stat__text">days left</p>
    </div>

    <div class="stats__meter">
      <Meter :value=getPercentage() />
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import Meter from './reusable/Meter.vue';

export default {
  name: 'Stats',
  components: {
    Meter,
  },
  computed: {
    stats() {
      return this.getStats();
    },
    backed() { return this.format(this.stats.backed); },
    backers() { return this.format(this.stats.backers); },
    daysLeft() { return this.format(this.stats.daysLeft); },
    target() { return this.format(this.stats.target); },
  },
  methods: {
    ...mapGetters(['getStats']),
    getPercentage() {
      const percentage = ((this.stats.backed / this.stats.target) * 100);
      return percentage <= 100 ? String(percentage) : '100';
    },
    format(number) {
      return new Intl.NumberFormat('en-US', { maximumSignificantDigits: 3 }).format(number);
    },
  },
};
</script>

<style lang="scss" scoped>
.stats {
  background-color: var(--white);
  box-shadow: 0 0 10px 1px rgba(0, 0, 0, 0.1);
  border-radius: var(--border-radius);
  padding: var(--bg-spacer) var(--sm-spacer);
  margin-top: var(--sm-spacer);
  max-width: var(--text-width);
  @media (min-width: 50em) {
    display: grid;
    grid-template-areas: "backed backers days-left"
                         "progress progress progress"
  }

  &__meter {
    padding-top: var(--bg-spacer);
    width: 100%;
    margin: 0 auto;
    grid-area: progress;
  }
}

.stat {
  &__title {
    font-size: calc(var(--fs-h3) + 1rem);
    line-height: 1;
    padding-bottom: calc(var(--sm-spacer) / 3);
    color: initial;
  }

  &__text {
    font-size: calc(var(--fs-h4) - 0.3rem);
  }
}

.stat + .stat {
  width: max-content;
  margin: 0 auto;

  border-top: 1px solid var(--dark-gray);
  padding-top: calc(var(--bg-spacer) / 1.2);
  margin-top: calc(var(--bg-spacer) / 1.2);
  @media (min-width: 50em) {
    border-top: unset;
    width: unset;
    margin: unset;

    border-left: 1px solid var(--dark-gray);
    padding: 0 1rem;
  }
}
</style>
