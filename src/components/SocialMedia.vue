<script setup>
function openLink(url) {
  window.open(url, '_blank');
}
</script>

<template>
  <div class="content">
    <div class="content_block">
      <section class="content_block_buttons">
        <font-awesome-icon id="icon" icon="fa-brands fa-tiktok" @click="openLink('https://www.tiktok.com/@roughlesbh')"/>
        <font-awesome-icon id="icon" icon="fa-brands fa-youtube" @click="openLink('https://www.youtube.com/@RoughlesBH')"/>
        <font-awesome-icon id="icon" icon="fa-brands fa-twitch" @click="openLink('https://www.twitch.tv/roughlesbh')"/>
        <font-awesome-icon id="icon" icon="fa-brands fa-x-twitter" @click="openLink('https://x.com/RoughlesBH')"/>


      </section>
      <div class="content_block_display">
        <iframe width="900px" height="506.25px" src="https://www.youtube.com/embed/aaEkwktCYYs" title="Brawlhalla Team Combo Madness" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
        <!-- <img src="/src/assets/photos/BHRenders/Couch_Characters.avif"> -->
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

.content{
  width: 100%;
  align-items: center;
  justify-content: center;
  //background: rgba($color: #000000, $alpha: 0.4);
  margin-bottom: 30px;
  z-index: 1;
  &_block{
    margin: 30px auto;
    //background: rgba($color: #000000, $alpha: 0.4);
    &_buttons{
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 6vw;
      max-height: 80px;
      background: #0a0b13;
      margin-bottom: 5px;
      text-align: center;
      clip-path: polygon(0% 0%, 98% 0%, 100% 30%, 100% 100%, 0% 100%);
      #icon{
        margin: 0 auto;
        font-size: 4vw;
        color: #e8e8e8; // Yellow: #e5cc70;
        padding: 1.1vw 30px;
        transition: padding 0.4s ease, filter 0.4s ease;
        &:hover{
          filter: drop-shadow(1px 1px 5px #ffffdd);
          padding: 1.1vw 45px;
          cursor: pointer;
        }
      }
    }
    &_display{
      width: 100%;
      background: #0a0b13;
      iframe{
        aspect-ratio: 16 / 9;
        width: 100%;
        height: auto;
      }
      img{
        width: 20%;
        margin: 10px 0px;
      }
    }
  }
}

@media only screen and (max-width: 1440px) {
  
}

@media only screen and (min-width: 1270px) {
  .content{
    &_block{
      &_buttons{
        #icon{
          font-size: 55px;
        }
      }
    }
  }
}

@media only screen and (max-width: 1270px) {
  
}


</style>