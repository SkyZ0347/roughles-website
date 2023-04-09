<script setup>

</script>

<template>
  <header>
    <h1 id="tytuł">Marecki</h1>
    <h3>Wykończenia wnętrz</h3>
  </header>
  <main class="content">
    <div class="content_main">
      <img src="./assets/photos/placeholder main.jpg">
      <h1>Tytuł</h1>
      <p>Opis przykładowy do zmiany</p>
    </div>
    <div class="content_editor">
      <img src="./assets/photos/placeholder1.jpg">
    </div>

    <div class="content_contact">
      <h1 class="contect_contact_text">KONTAKT</h1>
      <div class="content_contact_blocks">
        <div class="content_contact_blocks_phone">
          <img src="./assets/icons/phone.png">
          <h1>661761799</h1>
        </div>
        <div class="content_contact_blocks_name">
          <img src="./assets/icons/name.png">
          <h1>Marek Walkowiak</h1>
        </div>
        <div class="content_contact_blocks_fb">
          <img src="./assets/icons/facebook.png">
          <h1>Facebook</h1>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
*{
  font-family: 'Fredoka', sans-serif;
  font-family: 'Quicksand', sans-serif;
  user-select: none;
}
header{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 9999;
  height: 10vh;
  background-color: #205F59;
}
.content{
  &_main{
    
  }
}
.mainblock{
  position: relative;
  overflow: hidden;
  height: 80vh;
}
#main{
  margin-top: 10vh;
  background-image: linear-gradient(to right, rgba(255, 255, 255, 0), rgba(255, 255, 255, 1));
}
#main img{
  position: absolute;
  top: 0;
  left: 0;
  transform: translateY(-20%);
  object-fit: cover;
}
#main::after{
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: linear-gradient(110deg  , rgba(0, 0, 0, 0), rgba(0, 0, 0, 1));
  z-index: 1;
}
#main h1{
  font-size: 70px;
  color: white;
  position: relative;
  text-align: right;
  top: 3vw;
  right: 3vw;
  z-index: 2;
}
#main p{
  font-size: 30px;
  color: white;
  position: relative;
  text-align: right;
  top: 3vw;
  right: 3vw;
  z-index: 2;
}
#editor{
  background: #58B9AF;
}
#editor img{
  height: 50vh;
  margin: 5vh;
}
#kontakt{
  height: 30vh;
  background: #E2F3F1;
}
#kontaktbloki{
  display: flex;
  justify-content: center;
}
#text{
  color: black;
}
#kontakt h1{
  margin: 4vh 0vh 2vh 0vh;
  text-align: center;
}
#kontaktbloki div{
  margin: 0;
  padding: 0vh;
  width: 40vh;
  height: 10vh;
  margin: 2vh;
  background: #58B9AF;
  border-radius: 15px;
  display: flex;
}
#kontaktbloki div:first-child{
  width: 27vh;
}
#kontaktbloki div:last-child{
  width: 27.3vh;
}
#nrtel:hover, #fb:hover{
  background: #38A499;
}
#kontakt div img{
  height: 8vh;
  margin: 1vh;
}
#kontakt div h1{
  color: black;
  font-size: 30px;
  margin: 2.2vh 0vh 0vh 0vh;
}
</style>