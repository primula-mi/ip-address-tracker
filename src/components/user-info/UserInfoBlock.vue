<script setup>
// import UserInfoItem from "@/components/user-info/UserInfoItem.vue";
const props = defineProps(["userData"]);
console.log("userData",props.userData);
</script>
<template>
    <div class="user-ip-info">
        <ul class="user-ip-info__list">
            <li class="user-ip-info__item">
                <span class="user-ip-info__title">ip address</span>
                <span class="user-ip-info__text">{{ props.userData.ip }}</span>
            </li>
            <li class="user-ip-info__item">
                <span class="user-ip-info__title">location</span>
                <span class="user-ip-info__text">{{ props.userData.city }}, {{ props.userData.region }} {{ props.userData.postal }}</span>
            </li>
            <li class="user-ip-info__item">
                <span class="user-ip-info__title">timezone</span>
                <span class="user-ip-info__text">UTC {{ props.userData.timezone.utc }}</span>
            </li>
            <li class="user-ip-info__item">
                <span class="user-ip-info__title">isp</span>
                <span class="user-ip-info__text">{{ props.userData.connection.isp }}</span>
            </li>
        </ul>
    </div>
</template>

<style scoped>
.user-ip-info {
    width: 75%;
    background: var(--color-white);
    padding: 1.5rem 1.2rem;
    border-radius: var(--border-radius-base);
}
@media(max-width: 576px) {
    .user-ip-info {
        width: 90%;
    }
}
.user-ip-info__list {
    margin: 0;
    padding: 0;
    list-style: none;
    display: flex;
}
@media(max-width: 375px) {
    .user-ip-info__list {
        flex-direction: column;
        align-items: center;
    }
}

.user-ip-info__item:not(:first-child) {
    padding: 0 0 0 1rem;
}
@media(max-width: 576px) {
    .user-ip-info__item:not(:first-child) {
        padding: 0 0 0 0.4rem;
    }
}
@media(max-width: 375px) {
    .user-ip-info__item:not(:first-child) {
        margin: 0.5rem 0 0;
        padding: 0;
    }
}
.user-ip-info__item {
    display: flex;
    flex-direction: column;
    width: calc(100% / 4);
    /* padding: 0 1rem; */
}
@media(max-width: 375px) {
    .user-ip-info__item {
        width: 100%;
        text-align: center;
    }
}
.user-ip-info__item:not(:last-child) {
    border-right: 1px solid var(--color-dark-gray);
}
@media(max-width: 375px) {
    .user-ip-info__item:not(:last-child) {
        border-right: none;
    }
}
.user-ip-info__title {
    font-size: 0.5rem;
    color: var(--color-dark-gray);
    text-transform: uppercase;
    font-weight: var(--fint-weight-medium);
    letter-spacing: 0.05rem;
}
.user-ip-info__text {
    font-weight: var(--fint-weight-medium);
}
@media(max-width: 776px) {
    .user-ip-info__text {
        font-size: 0.9rem
    }
}
@media(max-width: 576px) {
    .user-ip-info__text {
        font-size: 0.8rem
    }
}
@media(max-width: 476px) {
    .user-ip-info__text {
        font-size: 0.7rem
    }
}
@media(max-width: 375px) {
    .user-ip-info__text {
        font-size: 1rem
    }
}
</style>