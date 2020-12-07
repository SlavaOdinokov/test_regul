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

          <form
            class="review-form"
            enctype="multipart/form-data"
          >
            <div class="review-form__rating">
              <Rating
                v-for="ratingItem in ratingItems"
                :key="ratingItem.name"
                :ratingItem="ratingItem"
                @sendRating="getRating"
              />
            </div>

            <div class="review-form__comment">
              <textarea
                class="review-form__comment-field"
                name="comment"
                placeholder="Комментарий"
                :maxlength="maxLengthComment"
                v-model="textComment"
              >
              </textarea>
              <span class="review-form__comment-counter">{{textComment.length}}/{{maxLengthComment}}</span>
            </div>

            <div class="review-form__upload-img">
              <input
                class="review-form__upload-img-input"
                id="upload-img"
                type="file"
                name="uploadImg"
                accept="image/*"
                multiple
                ref="files"
              >
              <label for="upload-img" class="review-form__upload-img-label" title="Upload file"></label>
              <div class="review-form__upload-img-preview">
                <img src="/images/foto_1.jpg" alt="foto" />
                <span class="review-form__delete-img"></span>
              </div>
              <div class="review-form__upload-img-preview">
                <img src="/images/foto_2.jpg" alt="foto" />
                <span class="review-form__delete-img"></span>
              </div>
              <div class="review-form__upload-img-preview">
                <img src="/images/foto_3.jpg" alt="foto" />
                <span class="review-form__delete-img"></span>
              </div>
              <div class="review-form__upload-img-preview">
                <img src="/images/foto_4.jpg" alt="foto" />
                <span class="review-form__delete-img"></span>
              </div>
            </div>

            <div class="review-form__btn">
              <button @click.prevent="submiteForm" class="btn">Отправить</button>
            </div>
          </form>

        </div>
      </div>
    </transition>

    <Notifications
      :messages="messages"
    />
  </div>
</template>

<script>
  import Rating from '@/components/Rating'
  import Notifications from '@/components/Notifications'

  export default {
    name: 'reviews',
    components: { Rating, Notifications },
    data() {
      return {
        isPopup: false,
        ratingItems: [
          { title: 'Скорость', name: 'speed' },
          { title: 'Скорость отдачи видео', name: 'video-speed' },
          { title: 'Качество', name: 'quality' },
          { title: 'Пунктуальность', name: 'punctuality' }
        ],
        maxLengthComment: 500,
        textComment: '',
        rating: [],
        messages: []
      }
    },
    methods: {
      closePopup() {
        this.isPopup = false
      },
      getRating(data) {
        if (this.rating.length > 0) {
          if (!this.rating.find(item => item === data)) {
            this.rating.push(data)
          }
        } else {
          this.rating.push(data)
        }
      },
      submiteForm() {
        if (this.checkForm()) {
          const timeStamp = Date.now().toLocaleString()

          this.messages.unshift(
            { name: 'Спасибо, отзыв опубликован!', type: 'success', id: timeStamp }
          )
          this.closePopup()
          this.textComment = ''
        }
      },
      checkForm() {
        const timeStamp = Date.now().toLocaleString()

        if (this.rating.length !== 4) {
          this.messages.unshift(
            { name: 'Поставьте рейтинг', type: 'error', id: timeStamp }
          )
          return false
        }
        if (!this.textComment) {
          this.messages.unshift(
            { name: 'Заполните поле комментарий', type: 'error', id: timeStamp }
          )
          return false
        }
        if (this.$refs.files.files.length === 0) {
          this.messages.unshift(
            { name: 'Загрузите фото', type: 'error', id: timeStamp }
          )
          return false
        }
        return true
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
      padding: 0 32px;
      margin-bottom: 28px;
    }
    &__comment {
      height: 100px;
      padding: 0 32px;
      margin-bottom: 36px;
      position: relative;
    }
    &__comment-field {
      display: block;
      width: 100%;
      height: 100px;
      margin-bottom: 36px;
      padding: 12px;
      outline: none;
      resize: none;
      border: 1px solid #EAECF0;
      border-radius: 6px;
      background: #FAFAFA;
      font-family: 'Montserrat', sans-serif;
      font-weight: 400;
      font-size: 16px;
      line-height: 24px;
      color: #7f899e;
      opacity: .9;
    }
    &__comment-counter {
      position: absolute;
      bottom: -20px;
      right: 32px;
      font-size: 12px;
      line-height: 16px;
      font-weight: 400;
      color: #7f899e;
      opacity: .9;
    }
    &__upload-img {
      position: relative;
      margin-bottom: 12px;
      padding: 0 32px;
      display: flex;
      flex-wrap: wrap;
    }
    &__upload-img-input {
      position: absolute;
      width: 1px;
      height: 1px;
      overflow: hidden;
      opacity: 0;
    }
    &__upload-img-label {
      margin-right: 8px;
      margin-bottom: 12px;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 80px;
      height: 80px;
      background: #F3F4F6;
      border: 1px solid #EAECF0;
      border-radius: 6px;
      cursor: pointer;

      &:before {
        content: url(/images/icons/plus.svg);
        width: 14px;
        height: 14px;
      }
    }
    &__upload-img-preview {
      margin-right: 8px;
      margin-bottom: 12px;
      width: 80px;
      height: 80px;
      border-radius: 6px;
      position: relative;

      /* &:hover + &__delete-img {
        opacity: 1;
      } */
    }
    &__delete-img {
      position: absolute;
      top: 8px;
      right: 8px;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 32px;
      height: 32px;
      background: rgba(0, 0, 0, 0.6);
      border-radius: 4px;
      opacity: 0;
      cursor: pointer;
      transition: .2s;

      &:before {
        content: url(/images/icons/delete.svg);
      }
    }
    &__upload-img-preview:hover &__delete-img {
      opacity: 1;
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
