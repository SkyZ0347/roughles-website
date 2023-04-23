<script setup>
import Painting from '../components/MareckiPainting.vue'
</script>

<template>
  <main class="content">
    <div class="content_main">
      <Painting />
      <img src="../assets/photos/placeholder main.jpg">
      <h1>Tytuł</h1>
      <p>Opis przykładowy do zmiany</p>
    </div>
    <!-- <div class="content_editor">
      <img src="../assets/photos/placeholder1.jpg">
    </div> -->
  </main>
</template>

<style scoped lang="scss">
.content{
  &_main{
    width: 100%;
    margin: 100px 0px 0px 0px;
    padding: 0;
    transition: margin-top 0.5s ease;
    overflow: hidden;
    &:after{
      content: '';
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background: linear-gradient(110deg  , rgba(0, 0, 0, 0), rgba(0, 0, 0, 1));
    }
    img{
      width: 100%;
    }
    h1{
      font-size: 5vw;
      color: #E2F3F1;
      position: absolute;
      text-align: right;
      top: 2vh;
      right: 4vw;
      z-index: 2;
    }
    p{
      font-size: 2vw;
      color: #E2F3F1;
      position: absolute;
      text-align: right;
      top: 11vw;
      right: 4vw;
      z-index: 2;
    }
  }
  &_editor{
    //position: absolute;
    margin-top: -10px;
    background: #58B9AF;
    z-index: 1;
    img{
      height: 50vh;
      margin: 5vh;
    }
  }
}

@media only screen and (max-width: 700px){
  .content_main{
    margin-top: 70px;
  }
}
</style>