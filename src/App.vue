<script setup>
import { ref, onBeforeMount } from 'vue';
import PageTitle from "@/components/PageTitle.vue";
import SearchForm from "@/components/search-form/SearchForm.vue";
import UserInfoBlock from "@/components/user-info/UserInfoBlock.vue";
import FooterBlock from "@/components/FooterBlock.vue";
import MapBlock from "@/components/MapBlock.vue";
import PopupBlock from "@/components/PopupBlock.vue";

const titleText = "IP Address Tracker";
const searchInputPlaceholderText = "Search for any IP address or domain";
let userInfoBlock = ref("");
let mapInfo = ref("");
let notification = ref("");

const searchUserIp = async (event) => {
  const data = await getUserInfo(event);
  renderComponents(data);
};
const getUserInfo = async (ip = "") => {
  const url = `https://ipwho.is/${ip}`;
  const result = await sendFetchRequest(url);
  return result;
};
const sendFetchRequest = async (url) => {
  const result = await fetch(url).then((r) => r.json());
  return result;
};
const renderMap = (lat, long) => {
  mapInfo.value = [lat, long];
}
const renderUserInfo = (data) => {
  userInfoBlock.value = data;
}
const renderNotificationInfo = (data) => {
  notification.value = data;
}
const renderComponents = (data) => {
  if (data.success) {
    renderMap(data.latitude, data.longitude);
    renderUserInfo(data);
  } else {
    renderNotificationInfo(data);
    setTimeout(() => {
      renderNotificationInfo("");
    }, 2000);
  }
  
}
onBeforeMount( async () => {
  const data = await getUserInfo("");
  renderComponents(data);
});
</script>

<template>
  <main>
    <div class="header">
      <PopupBlock :notification="notification"/>
      <PageTitle :text="titleText"/>
      <SearchForm :placeholderText="searchInputPlaceholderText" @searchUserIp="searchUserIp"/>
      <UserInfoBlock :userData="userInfoBlock"/>
    </div>
    <MapBlock :mapData="mapInfo"/>
  </main>
  <FooterBlock/>
  
</template>

<style scoped>
  .header {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
    z-index: 3;
    padding: 1.25rem;
    background: url(/src/assets/images/bg/pattern-bg-desktop.png) no-repeat top center / cover;
  }
  @media(max-width: 375px) {
    .header {
      background: url(/src/assets/images/bg/pattern-bg-mobile.png) no-repeat top center / cover;
    }
  }
  .header .title {
    margin: 0 0 1rem;
  }
  .user-ip-info{
    position: absolute;
    top: 8rem;
    z-index: 5;
  }

  .drop-down-enter-active {
    transition: all 0.3s ease-out;
  }

  .drop-down-leave-active {
    transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
  }

  .drop-down-enter-from,
  .drop-down-leave-to {
    transform: translateY(-20px);
    opacity: 0;
  }
</style>

