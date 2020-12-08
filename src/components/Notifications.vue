<template>
  <div class="notifications">
    <transition-group name="notifications">
      <div
        v-for="(message, index) in messages"
        :key="message.id"
        class="notifications__content"
        :class="message.type"
      >
        <div class="notifications__message">{{message.name}}</div>
        <div @click="closeMessage(index)" class="notifications__close"></div>
      </div>
    </transition-group>
  </div>
</template>

<script>
  export default {
    name: 'notifications',
    props: {
      messages: {
        type: Array,
        default() {
          return []
        }
      }
    },
    methods: {
      hideNotification() {
        if (this.messages.length) {
          setTimeout(() => {
            this.messages.splice(this.messages.length - 1, 1)
          }, 3000)
        }
      },
      closeMessage(index) {
        this.messages.splice(index, 1)
      }
    },
    watch: {
      messages() {
        this.hideNotification()
      }
    },
    mounted() {
      this.hideNotification()
    }
  }
</script>

<style lang="scss">
  .notifications {
    width: 280px;
    position: fixed;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 2;

    &__content {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0px 12px;

      height: 36px;
      border-radius: 6px;
      font-weight: 500;
      font-size: 14px;
      line-height: 20px;
      color: #FFFFFF;
      margin-bottom: 10px;

      &.success { background: #15A758; }
      &.error { background: #a82929; }
    }
    &__message {
      margin-right: 12px;
    }
    &__close {
      width: 24px;
      height: 24px;
      background-image: url(/images/icons/cancel.svg);
      background-repeat: no-repeat;
      cursor: pointer;
    }

    .notifications {
      &-enter, &-leave-to { transform: translateY(-20px); opacity: 0; }
      &-enter-active, &-leave-active { transition: all .5s; }
      &__enter-to, &-leave { opacity: 1; }
      &-move { transition: all .5s; }
    }

    @media (min-width: 576px) {
      top: 30px;
    }
  }
</style>
