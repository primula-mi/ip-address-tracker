<script setup>
    const props = defineProps(["notification"]);
</script>

<template>
    <Transition name="drop-down">
        <div class="notification" :class="(props.notification.success) ? 'success' : 'error'" v-if="props.notification.message">
            <div class="notification__text">{{ props.notification.message }}</div>
        </div>
    </Transition>
</template>

<style scoped>
.notification {
    position: fixed;
    right: 0;
    margin: 0 1%;
    min-width: 20%;
    padding: 1rem 2rem;
    background: var(--color-white);
    z-index: 15;
    border-radius: var(--border-radius-base);
    text-align: center;
}
@media(max-width: 375px) {
    .notification {
        margin: -5% 10%;
        right: 0;
        left: 0;
    }
  }
.error {
    background: #ff6347;
}
.success {
    background: #90ee90;
}
</style>