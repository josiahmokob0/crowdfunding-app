<template>
  <div class="reward" :class="{'reward--empty': reward.left == 0}">
    <div class="reward__header">
      <h3 class="reward__title">{{reward.title}}</h3>
      <p class="reward__sub-title">{{reward.text}}</p>
    </div>
    <p class="reward__description">{{reward.description}}</p>
    <div class="reward__footer">
      <div class="reward__left">
        <span class="left">{{reward.left}}</span> left
      </div>
      <div class="reward__select">
        <cbutton
          :value="reward.left > 0 ? 'Select Reward' : 'Out of stock'"
          :click="handleClick"
          :className="{'button--empty': reward.left == 0}"
          :disabled="reward.left == 0"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';
import cbutton from './reusable/Button.vue';

export default {
  props: {
    reward: Object,
  },
  components: {
    cbutton,
  },
  methods: {
    handleClick() {
      this.toggleRewardModal();
      this.setCurrentId(this.reward.id);
      /*
       - Looks like a hack, I am scrolling to the top on behave of the user
       - I am sure there is a better way [ to future me ] other than using the window object.
      */
      window.location.href = '#top';
    },
    ...mapActions(['toggleRewardModal', 'setCurrentId']),
  },
};
</script>

<style lang="scss">
.reward {
  background-color: var(--white);
  box-shadow: 0 0 3px 1px var(--gray);
  border-radius: var(--border-radius);
  padding: var(--sm-spacer) var(--bg-spacer);
  margin-top: var(--sm-spacer);

  &--empty {
    opacity: 0.5;
  }

  &__title {
    font-size: var(--fs-h3);
    padding-bottom: calc(var(--sm-spacer) / 5);
    line-height: 1;
    color: initial;
  }

  &__description {
    padding-bottom: var(--sm-spacer);
  }

  &__header {
    padding-bottom: var(--sm-spacer);
    @media (min-width: 50em) {
      display: flex;
      justify-content: space-between;
    }
  }

  &__sub-title {
    color: var(--moderate-cyan);
    font-weight: 700;
  }

  &__footer {
    @media (min-width: 50em) {
      display: flex;
      justify-content: space-between;
    }
  }

  &__left {
    display: flex;
    align-items: center;
    column-gap: calc(var(--sm-spacer) / 3);
    margin-bottom: var(--sm-spacer);
    @media (min-width: 50em) {
      margin-bottom: 0;
    }
    .left {
      font-size: var(--fs-h3);
      font-weight: bold;
      color: initial;
    }
  }
}
</style>
