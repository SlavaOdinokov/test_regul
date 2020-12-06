<template>
  <div class="rating">
    <p class="rating__name">{{ ratingItem.title }}</p>
    <div class="rating__group">
      <input class="rating__input" type="radio" :name="ratingItem.name" :id="`${ratingItem.name}-1`" value="1">
      <label class="rating__star" :for="`${ratingItem.name}-1`"></label>

      <input class="rating__input" type="radio" :name="ratingItem.name" :id="`${ratingItem.name}-2`" value="2">
      <label class="rating__star" :for="`${ratingItem.name}-2`"></label>

      <input class="rating__input" type="radio" :name="ratingItem.name" :id="`${ratingItem.name}-3`" value="3">
      <label class="rating__star" :for="`${ratingItem.name}-3`"></label>

      <input class="rating__input" type="radio" :name="ratingItem.name" :id="`${ratingItem.name}-4`" value="4">
      <label class="rating__star" :for="`${ratingItem.name}-4`"></label>

      <input class="rating__input" type="radio" :name="ratingItem.name" :id="`${ratingItem.name}-5`" value="5">
      <label class="rating__star" :for="`${ratingItem.name}-5`"></label>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'rating',
    props: {
      ratingItem: {
        type: Object,
        default() {
          return {}
        }
      }
    },
    data() {
      return {}
    },
    computed: {},
    methods: {}
  }
</script>

<style lang="scss">
  .rating {
    padding: 0 32px;
    margin-bottom: 34px;

    &__name {
      margin-bottom: 8px;
      font-weight: 500;
      font-size: 14px;
      line-height: 20px;
    }
    &__group {
      position: relative;
      background-image: url(/images/icons/star_empty.svg);
      background-size: 32px 32px;
      background-repeat: repeat-x;
      width: 160px;
      height: 32px;
      cursor: pointer;
    }
    &__input {
      position: absolute;
      width: 1px;
      height: 1px;
      overflow: hidden;
      clip: rect(0 0 0 0);
    }
    &__star {
      appearance: none;
      position: absolute;
      top: 0;
      left: 0;
      height: 32px;
      background-size: 32px 32px;
      background-repeat: repeat-x;
      cursor: pointer;

      &:nth-of-type(1) { width: calc(32px*1); z-index: 5; }
      &:nth-of-type(2) { width: calc(32px*2); z-index: 4; }
      &:nth-of-type(3) { width: calc(32px*3); z-index: 3; }
      &:nth-of-type(4) { width: calc(32px*4); z-index: 2; }
      &:nth-of-type(5) { width: calc(32px*5); z-index: 1; }
    }

    &__input:checked + &__star, &__star:hover {
      background-image: url(/images/icons/star_active.svg);
    }
    &__star:hover ~ &__star {
      background-image: url(/images/icons/star_empty.svg);
    }
  }
</style>
