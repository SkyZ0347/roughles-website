<script setup>
document.addEventListener('DOMContentLoaded', function() {
  var copytext = document.getElementById("copynumber");
  var edittext = document.getElementById("edittext");
  // document.getElementById("phonenumber").addEventListener("mouseover", function() { copytext.style.display = "block" });
  document.getElementById("phonenumber").addEventListener("mouseout", function() { 
    copytext.style.display = "none";
    copytext.style.animationPlayState = "paused";
    edittext.innerHTML = "Skopiuj";
    i = 5;
  });
  document.getElementById("phonenumber").addEventListener("click", function () { 
    fallbackCopyTextToClipboard("661761799");
    if (i == 5) {edittext.innerHTML = "Skopi";}
    typeWriter();
  });

  var speed = 100;
  var textdocelowy = "Skopiowano";
  var i = 5;

  function typeWriter() {
  if (i < textdocelowy.length) {
    edittext.innerHTML += textdocelowy.charAt(i);
    i++;
    setTimeout(typeWriter, speed);
  }
}

  function fallbackCopyTextToClipboard(text) {
    //animation
    copytext.style.animationPlayState = "running";
    
    //functionality
  var textArea = document.createElement("textarea");
  textArea.value = text;
  
  // Avoid scrolling to bottom
  textArea.style.top = "0";
  textArea.style.left = "0";
  textArea.style.position = "fixed";

  document.body.appendChild(textArea);
  textArea.focus();
  textArea.select();

  try {
    document.execCommand('copy');
  } catch (err) {
    console.error("Nie udało się skopiować do schowka.")
  }

  document.body.removeChild(textArea);
}

});
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
      <h1 class="content_contact_text">KONTAKT</h1>
      <div class="content_contact_blocks">
        <div class="content_contact_blocks_phone" id="phonenumber">
          <img src="./assets/icons/phone.png">
          <h2>661761799</h2>
          <div class="content_contact_blocks_phone_copy" id="copynumber">
            <h1><span id="edittext">Skopiuj</span></h1>
          </div>
        </div>
        <div class="content_contact_blocks_name">
          <img src="./assets/icons/name.png">
          <h2>Marek Walkowiak</h2>
        </div>
        <div class="content_contact_blocks_fb">
          <img src="./assets/icons/facebook.png">
          <h2>Facebook</h2>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped lang="scss">
*{
  font-family: 'Fredoka', sans-serif;
  font-family: 'Quicksand', sans-serif;
  user-select: none;
}
header{
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  z-index: 9999;
  height: 10vh;
  background-color: #205F59;
  h1{
    font-size: 4vh;
    margin-left: 1vw;
  }
  h3{
    font-size: 1.7vh;
    margin-left: 1vw;
  }
}
.content{
  &_main{
    width: 100vw;
    height: 100%;
    position:relative;
    margin-top: 10vh;
    overflow: hidden;
    &:after{
      content: '';
      width: 100vw;
      height: 100vh;
      position: absolute;
      top: 0;
      left: 0;
      background: linear-gradient(110deg  , rgba(0, 0, 0, 0), rgba(0, 0, 0, 1));
    }
    img{
      width: 100vw;
    }
    h1{
      font-size: 7vh;
      color: #E2F3F1;
      position: absolute;
      text-align: right;
      top: 2vh;
      right: 4vw;
      z-index: 2;
    }
    p{
      font-size: 3vh;
      color: #E2F3F1;
      position: absolute;
      text-align: right;
      top: 13vh;
      right: 4vw;
      z-index: 2;
    }
  }
  &_editor{
    background: #58B9AF;
    img{
      height: 50vh;
      margin: 5vh;
    }
  }
  &_contact{
    background: #E2F3F1;
    height: 30vh;
    margin: 0;
    overflow: hidden;
    &_text{
      color: black;
      text-align: center;
      padding: 4vh 0vw 2vh 0vw;
    }

    // margin-top: 0px;
    // height: 30vh;
    // background: #E2F3F1;
    // &_blocks{
    //   display: flex;
    //   justify-content: center;
    //   div{
    //     margin: 0;
    //     padding: 0vh;
    //     width: 24.4vw;
    //     height: 10vh;
    //     margin: 2vw;
    //     background: #58B9AF;
    //     border-radius: 15px;
    //     display: flex;
    //     &:nth-child(2){
    //       width: 16.7vw !important;
    //     }
    //     &:last-child{
    //       width: 17vw !important;
    //     }
    //     img{
    //       height: 8vh;
    //       margin: 1vh;
    //     }
    //     h2{
    //       color: black;
    //       font-size: 30px;
    //       margin: 2.2vh 0vh 0vh 0vh;
    //     }
    //   }
    //   &_phone:hover, &_fb:hover{
    //     background: #38A499;
    //   }
    // }
  }
}

// #copynumber{
//   height: 37px !important; 
//   width: 100px !important;
//   // margin: -0.85vh 6vw 0vh 0vw !important;
//   border-radius: 15px;
//   border-bottom-left-radius: 0px !important;
//   background: #184540 !important; 
//   position: relative !important;
//   // display: nones;
//   animation-name: copieddiv;
//   animation-duration: 1s;
//   animation-fill-mode: forwards;
//   animation-play-state: paused;
//   animation-iteration-count: 1;
//   h1{
//     color: #EBF7F6;
//     font-size: 23px;
//     padding: 0vh 0vh 0vh 1.3vh;
//     display:inline;
//   }
// }
// #edittext{
//   color: #EBF7F6;
//   font-size: 23px;
//   padding: 0vh 0vh 0vh 0vh;
//   display:inline;
// }
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