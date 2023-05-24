<script setup>
import { ref, onBeforeMount } from 'vue';
import PageTitle from "@/components/PageTitle.vue";
import SearchForm from "@/components/search-form/SearchForm.vue";
import UserInfoBlock from "@/components/user-info/UserInfoBlock.vue";
import FooterBlock from "@/components/FooterBlock.vue";
import MapBlock from "@/components/MapBlock.vue";

const titleText = "IP Address Tracker";
const searchInputPlaceholderText = "Search for any IP address or domain";
let userInfoBlock = ref(undefined);
let mapInfo = ref(undefined);

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
const renderComponents = (data) => {
  renderMap(data.latitude, data.longitude);
  renderUserInfo(data);
}
onBeforeMount( async () => {
  const data = await getUserInfo("");
  renderComponents(data);
});
</script>

<template>
  <main>
    <div class="header">
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
</style>

