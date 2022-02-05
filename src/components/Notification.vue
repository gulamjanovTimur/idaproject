<template>
  <div :class="{ 'notification--active': isActive }" class="notification">
    <div class="notification__text">{{ text }}</div>
    <img src="../assets/images/done.svg" class="notification__icon" />
  </div>
</template>
<script>
export default {
  name: "Notification",
  props: {
    text: {
      type: String,
      default: () => "text",
    },
    isActive: {
      type: Boolean,
      default: () => false,
    },
  },
};
</script>

<style lang="scss" scoped>
.notification {
  position: fixed;
  top: 0px;
  transform: translateY(-64px);
  right: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #2fa71c;
  color: #fff;
  width: fit-content;
  max-width: 300px;
  padding: 20px;
  border-radius: 16px;
  transition: 0.3s;
  &__text {
    font-size: 16px;
    margin-right: 20px;
  }
  &--active {
    transform: translateY(10px);
  }
}
</style>
