<template>
  <div class="reviews">
    <button
      class="btn"
      @click="isPopup = true"
    >
      Оставить отзыв
    </button>

    <transition name="transition-popup">
      <div
        class="popup-wrapper"
        v-if="isPopup"
      >
        <div class="popup">
          <div class="popup__header">
            <div class="popup__title">Мой отзыв</div>
            <div
              class="popup__close"
              @click="closePopup"
            >
              <img src="/images/icons/close.svg" alt="close">
            </div>
          </div>

          <div class="card-user">
            <img class="card-user__img" src="/images/foto_main.jpg" alt="photo">
            <div class="card-user__desc">
              <div class="card-user__title popup__title">Фоточки в свадебном платьице</div>
              <div class="card-user__name">Алена Смирнова</div>
            </div>
          </div>

          <form class="review-form">
            <div class="review-form__rating">
              <Rating
                v-for="ratingItem in ratingItems"
                :key="ratingItem.name"
                :ratingItem="ratingItem"
              />
            </div>
            <div class="review-form__btn">
              <button type="submite" class="btn">Отправить</button>
            </div>
          </form>

        </div>
      </div>
    </transition>

  </div>
</template>

<script>
  import Rating from '@/components/Rating'

  export default {
    name: 'reviews',
    components: { Rating },
    data() {
      return {
        isPopup: false,
        ratingItems: [
          { title: 'Скорость', name: 'speed' },
          { title: 'Скорость отдачи видео', name: 'video-speed' },
          { title: 'Качество', name: 'quality' },
          { title: 'Пунктуальность', name: 'punctuality' }
        ]
      }
    },
    computed: {},
    methods: {
      closePopup() {
        this.isPopup = false
      }
    }
  }
</script>

<style lang="scss">
  .popup-wrapper {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .4);
  }

  .popup {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 560px;
    /* height: 655px; */
    border-radius: 16px;
    background: #fff;

    &__header {
      margin-bottom: 24px;
      display: flex;
      justify-content: space-between;
      padding: 16px 21px 16px 32px;
      border-bottom: 1px solid #EAECF0;
    }
    &__title {
      font-size: 16px;
      font-weight: 600;
      line-height: 24px;
    }
    &__close {
      display: flex;
      align-items: center;
      cursor: pointer;
    }
  }

  .card-user {
    display: flex;
    margin-bottom: 32px;
    padding: 0 32px;

    &__img {
      border-radius: 6px;
      margin-right: 20px;
    }
    &__name {
      font-size: 12px;
      font-weight: 400;
      line-height: 16px;
      color: #50586A;
    }
  }

  .review-form {

    &__rating {
      display: flex;
      flex-wrap: wrap;
    }
    &__btn {
      border-top: 1px solid #EAECF0;
      padding: 16px;
      text-align: right;
    }
  }

  .transition-popup {
    &-enter, &-leave-to { opacity: 0; }
    &-enter-active, &-leave-active { transition: all .3s; }
    &-enter-to, &-leave { opacity: 1; }
  }
</style>
