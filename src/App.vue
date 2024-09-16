<script setup>
import { RouterView } from 'vue-router';

</script>

<template>
  <div id="content">
    <router-view></router-view>
    <!-- <router-view class="router-view" v-slot="{Component}">
      <Transition name="loteria" mode="out-in">
        <component :is="Component" />
      </Transition>
    </router-view> -->
  </div>
</template>

<style scoped lang="scss">

@font-face {
  font-family: Lato;
  src: url('/src/assets/LatoWeb-Bold.ttf');
}

@font-face {
  font-family: GrubyFont;
  src: url('/src/assets/BoldFont.ttf');
}

@font-face {
  font-family: BHFont;
  src: url('/src/assets/BHFont.otf');
}

*{
  //font-family: 'Fredoka', sans-serif;
  font-family: 'Lato';
  user-select: none;
}
#content{
  width: 100vw;
}

@media only screen and (max-width: 1920px) {
  
}
</style>