<script setup>
import PageHeader from "../components/PageHeader.vue";
import ONas from '../components/ONas.vue';
import SocialMedia from "../components/SocialMedia.vue";
import NasiGracze from "../components/NasiGracze.vue";
import ClanRewards from "../components/ClanRewards.vue";
import Footer from "../components/PageFooter.vue";

import { ref, computed } from 'vue';
defineProps(['navItems', 'style']);
//import { useRouter } from "vue-router";
//const router = useRouter();
const scrollTop = ref(0);

const handleScroll = () => {
  scrollTop.value = document.querySelector('.mainContent').scrollTop;
  //headerStyle();
};

// const headerStyle = () => {
//   const headr = document.querySelector('.headr');
//   const shadowIntensity = Math.min(scrollTop.value / 30, 1);

//   headr.style.boxShadow = `0 6px 4px rgba(0, 0, 0, ${0.7 * shadowIntensity})`;
//   headr.style.transition = 'box-shadow 0.3s ease';
// };

function scrollToElement(section) {
  const main = document.querySelector('.mainContent');
  section.style = 'filter: brightness(200%)';

  setTimeout(() => {
    section.style.transition = 'filter 1s ease';  // Add the transition
    section.style.filter = 'brightness(100%)';  // Change the brightness back to normal
  }, 100);

  const headerOffset = document.querySelector('.headr')?.offsetHeight || 0; // Example if there is a fixed header
  const elementPosition = section.getBoundingClientRect().top + window.scrollY;
  const offsetPosition = elementPosition - headerOffset;

  main.scrollTo({
    top: offsetPosition,  // Scroll to the calculated position
    behavior: 'smooth'  // Use smooth scrolling
 });
}

const handleO_NAS = () => {
  const section = document.querySelector('.onas');
  scrollToElement(section);
};

const handleSOCIAL_MEDIA = () => {
  const section = document.querySelector('.socialmedia');
  scrollToElement(section);
};

const handleGRACZE = () => {
  const section = document.querySelector('.nasigracze');
  scrollToElement(section);
};

// const handleNAGRODY = () => {
//   console.log('NAGRODY clicked');
//   router.push('/Loteria');
// };

const handleKONTAKT = () => {
  const section = document.querySelector('.kontakt');
  scrollToElement(section);
};

const navItemsPageOne = [
  { label: 'O NAS', action: handleO_NAS },
  { label: 'SOCIAL MEDIA', action: handleSOCIAL_MEDIA },
  { label: 'GRACZE', action: handleGRACZE },
  // { label: 'NAGRODY', action: handleNAGRODY },
  { label: 'KONTAKT', action: handleKONTAKT }
];


</script>

<template>
  <PageHeader :navItems="navItemsPageOne" class="headr" ref="header"></PageHeader>
  <main @scroll="handleScroll" class="mainContent">
    <div id="content">
      <ONas class="onas section" />
      <SocialMedia class="socialmedia section" />
      <ClanRewards ref="clanRewards" :scrollTop="scrollTop" />
      <NasiGracze class="nasigracze section" />
      <Footer class="kontakt section" />
    </div>
  </main>
</template>

<style scoped lang="scss">
#app {
  display: flex;
  flex-direction: column;
  height: 100%;
}

main {
  height: calc(100vh - 5.1rem);
  margin-top: 5.1rem;
  overflow-y: auto;
  overflow-x: hidden;
  scroll-behavior: smooth;
}

#content {
  width: 80vw;
  max-width: 1200px;
  height: 300px;
  margin: 0px auto;
}

.section {
  filter: brightness(100%);
}

@media only screen and (max-width: 800px) {
  main {
    margin-top: 0;
    top: 0;
  }
}
</style>