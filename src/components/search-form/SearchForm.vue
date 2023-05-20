<script setup>
import { ref } from 'vue';
const props = defineProps(["placeholderText"]);
const emits = defineEmits(["searchUserIp"]);
const userIpAddress = ref('');
// console.log(userIpAddress);
// const inputUserIp = (event) => {
//     userIpAddress.value += event.data;
//     console.log(userIpAddress);
// }
const searchUserIp = () => {
    console.log(userIpAddress.value);
    emits("searchUserIp", userIpAddress.value);
}
</script>
<template>
        <form class="search-form">
            <input class="search-form__input" type="text" :placeholder="props.placeholderText" v-model="userIpAddress" >
            
            <button class="search-form__btn" @click.prevent="searchUserIp">
                    <svg xmlns="http://www.w3.org/2000/svg" width="11" height="14"><path fill="none" stroke="#FFF" stroke-width="3" d="M2 1l6 6-6 6"/></svg>
            </button>
        </form>
</template>

<style scoped>
.search-form {
    display: flex;
}
@media (max-width: 375px) {
    .search-form {
        width: 90%;
        justify-content: center;
    }
};
.search-form__input {
    min-width: 350px;
    padding: 10px 15px;
    border: none;
    border-radius: 0.4rem 0 0 0.4rem;
    outline: none;
}
@media (max-width: 375px) {
    .search-form__input {
        min-width: 100%;
    }
};
.search-form__btn {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0.4rem 0.5rem;
    border: none;
    border-radius: 0 0.4rem 0.4rem 0;
    background: var(--color-very-dark);
}

.search-form__btn svg{
    
}

</style>