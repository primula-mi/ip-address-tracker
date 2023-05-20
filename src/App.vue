<script setup>
import { ref, onBeforeMount } from 'vue';
import PageTitle from "@/components/PageTitle.vue";
import SearchForm from "@/components/search-form/SearchForm.vue";
import UserInfoBlock from "@/components/user-info/UserInfoBlock.vue";
import FooterBlock from "@/components/FooterBlock.vue";
import MapBlock from "@/components/MapBlock.vue";

const titleText = "IP Address Tracker";
const searchInputPlaceholderText = "Search for any IP address or domain";
const searchUserIp = (event) => {
  console.log("event ",event);
  getUserInfo(event);
};
let userInfoBlock = ref(undefined);
let mapInfo = ref(undefined);
const getUserInfo = async (ip = "") => {
    const url = `http://ipwho.is/${ip}`;
    
    const data = await sendFetchRequest(url);
    mapInfo.value = [data.latitude, data.longitude];
    userInfoBlock.value = data;
    console.log("data",data);
};
const sendFetchRequest = async (url) => {
    let result = await fetch(url).then((r) => r.json());
    return result;
};
onBeforeMount(() => {
  getUserInfo("132.7.8.8");
})

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
  .header .title {
    margin: 0 0 1rem;
  }
  .user-ip-info{
    position: absolute;
    top: 8rem;
    z-index: 5;
  }
</style>

