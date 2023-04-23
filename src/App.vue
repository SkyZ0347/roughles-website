<script setup>
import Header from "./components/MareckiHeader.vue";
import Footer from "./components/MareckiFooter.vue";
</script>

<template>
  <Header />
  <RouterView />
  <Footer />
</template>

<style scoped lang="scss">
*{
  font-family: 'Fredoka', sans-serif;
  font-family: 'Quicksand', sans-serif;
  user-select: none;
}

@keyframes copieddiv{
  0%{
    width: 11vh;
    left: 38vh;
  }
  100%{
    width: 16.7vh;
    left: 32.3vh;
  }
}
@keyframes copiedtext{
  0%{ content: "Skopiuj"; }
  10%{ content: "Skopiu"; }
  20%{ content: "Skopio"; }
  30%{ content: "Skopiow"; }
  40%{ content: "Skopiowa"; }
  50%{ content: "Skopiowan"; }
  60%{ content: "Skopiowano"; }
  70%{ content: "Skopiowano"; }
  80%{ content: "Skopiowano"; }
  90%{ content: "Skopiowano"; }
  100%{ content: "Skopiowano"; }
}
@media only screen and (max-width: 1400px) {
  .content_contact_blocks_phone h2 {
    display: none;
  }
}
</style>