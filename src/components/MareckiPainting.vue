<script setup>

</script>

<template>
  <div class="content">
    <div class="content_roller">
      <div class="content_roller_head">
        <span></span>
        <span></span>
        <span></span>
      </div>
      <div class="content_roller_metal">
        <span></span>
        <span></span>
        <span></span>
        <span></span>
      </div>
      <div class="content_roller_handle">
        <span></span>
        <span></span>
      </div>
    </div>
    <div class="content_paint">
      <div class="content_paint_main">
        <span></span>
        <span></span>
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.content{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  z-index: 1;
  &_roller{
    position: absolute;
    width: 19vw;
    height: 20vw;
    $roller-top: 38vw;
    $roller-left: -2vw;
    $roller-tf: rotate(0deg) scale(1);
    top: $roller-top;
    left: $roller-left;
    transform: $roller-tf;
    animation: roller-move 2s 2s forwards infinite;
    z-index: 99;
    &_head{
      width: 15vw;
      height: 6vw;
      position: absolute;
      top: 2vw;
      left: 2vw;
      background: #60b6ad;
      border-radius: 1vw;
      z-index: 3;
      overflow: hidden;
      span{
        width: 22.5vw;
        height: 3vw;
        position: absolute;
        left: -3vw;
        background: #38a499;
        transform: rotate(25deg);
        z-index: 0;
        top: -1vw;
        animation-name: roll;
        animation-timing-function: linear;
        animation-duration: 1s;
        animation-iteration-count: infinite;
      }
      span:nth-child(2)
      {
        animation-delay: 0.33s;
      }
      span:nth-child(3)
      {
        animation-delay: 0.66s;
      }
    }
    &_metal{
      span{
        position: absolute;
        background: #919191;
        z-index: 0;
      }
      span:nth-child(1){
        width: 18vw;
        height: 1.125vw; //200px = 15vw
        top: 4.2502vw;
        left: 0.5vw;
        border-radius: 1.5vw 0.75vw 0.75vw 0vw;
      }
      span:nth-child(2){
        width: 1.125vw;
        height: 5.5vw;
        top: 4.5vw;
        left: 0.5vw;
        border-radius: 1.5vw 0vw 0vw 1.5vw;
      }
      span:nth-child(3){
        width: 10vw;
        height: 1.125vw;
        top: 9vw;
        left: 0.5vw;
        border-radius: 0vw 1.5vw 0vw 1.5vw;
      }
      span:nth-child(4){
        width: 1.125vw;
        height: 4vw;
        top: 10vw;
        left: 9.4vw;
      }
    }
    &_handle{
      span{
        position: absolute;
        z-index: 1;
      }
      span:nth-child(1){
        width: 1.875vw;
        height: 6vw;
        top: 13.5vw;
        left: 9vw;
        background: #393939;
      }
      span:nth-child(2){
        width: 0.375vw;
        height: 5.25vw;
        top: 13.9vw;
        left: 9.3vw;
        border-radius: 0.5vw;
        background: #ffffff;
        box-shadow: 0 0 0.225vw #fff;
      }
    }
    &:active{
      .content_paint_main span:nth-child(1){
        background-size: 100% 200%;
      }
    }
  }
  &_paint{
    &_main{
      span{
        width: 15vw;
        height: 85vh;
        position: absolute;
        background:#38a499;
        opacity: 0.3;
      }
      span:nth-child(1)
      {
        top: 84vh;
        left: 0vh;
        animation: paint-main-one 0.5s 2s forwards;
      }
      span:nth-child(2)
      {
        top: -111vh;
        left: 0vh;
        height: 102vh;
        animation: paint-main-two 0.5s 2.5s forwards;
        transform: rotate(-20deg);
      }
      span:nth-child(3)
      {
        top: 84vh;
        left: 15vw;
        animation: paint-main-one 0.5s 3s forwards;
      }
      span:nth-child(4)
      {
        top: -111vh;
        left: 30vw;
        height: 102vh;
        animation: paint-main-two-sec 0.5s 3.5s forwards;
        transform: rotate(-20deg);
      }
      span:nth-child(5)
      {
        top: 84vh;
        left: 30vw;
        animation: paint-main-one 0.5s 4s forwards;
      }
    }
  }
}

@keyframes paint-main-one{
  0% {
    top: 84vh;
  }
  100% {
    top: 0vh;
  }
}

@keyframes paint-main-two{
  0% {
    top: -111vh;
    left: -22vh;
  }
  100% {
    top: -9vh;
    left: 15.18vh;
  }
}

@keyframes paint-main-two-sec{
  0% {
    top: -111vh;
    left: 4.68vh;
  }
  100% {
    top: -9vh;
    left: 41.86vh;
  }
}

@keyframes roller-move{
  $roller-top: 10vw;
  0%{
    
  }
  50%{
    $roller-top: ($roller-top - 40vw);
    $roller-tf: rotate(0deg) scale(1.00);
  }
  55%{
    $roller-tf: rotate(-20deg) scale(0.96);
  }
  100%{
    $roller-top: $roller-top + 40.5vw;
    $roller-left: $roller-left + 17.5vw;
  }


  /* 0%{
    top: 38vw;
    left: -2vw;
  }
  20%{
    top: -8vw;
    left: -2vw;
    transform: rotate(0deg) scale(1.00);
  }
  23%{
    transform: rotate(-20deg) scale(0.96);
  }
  40%{
    top: 38.5vw;
    left: 15.5vw;
    transform: rotate(-20deg) scale(0.96);
  }
  43%{
    transform: rotate(0deg) scale(1.00);
  }
  60%{
    top: -8vw;
    left: 13vw;
    transform: rotate(0deg) scale(1.00);
  }
  63%{
    transform: rotate(-20deg) scale(0.96);
  }
  80%{
    top: 38.5vw;
    left: 31.3vw;
    transform: rotate(-20deg) scale(0.96);
  }
  83%{
    transform: rotate(0deg) scale(1.00);
    opacity: 1;
  }
  100%{
    top: -8vw;
    left: 28vw;
    opacity: 0;
  } */
}

@keyframes roll {
  0% {
    top: -5vw;
  }
  99% {
    top: 11vw;
  }
  100% {
    top: 11vw;
  }
}
</style>