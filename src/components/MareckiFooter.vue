<script setup>
document.addEventListener('DOMContentLoaded', function() {
  // var copydiv = document.getElementById("copy");
  // var copytext = document.getElementById("copy_text");





  // document.getElementById("phonenumber").addEventListener("mouseover", function() { copytext.style.display = "block" });
//   document.getElementById("phonenumber").addEventListener("mouseout", function() { 
//     copytext.style.display = "none";
//     copytext.style.animationPlayState = "paused";
//     edittext.innerHTML = "Skopiuj";
//     i = 5;
//   });
//   document.getElementById("phonenumber").addEventListener("click", function () { 
//     fallbackCopyTextToClipboard("661761799");
//     if (i == 5) {edittext.innerHTML = "Skopi";}
//     typeWriter();
//   });

//   var speed = 100;
//   var textdocelowy = "Skopiowano";
//   var i = 5;

//   function typeWriter() {
//   if (i < textdocelowy.length) {
//     edittext.innerHTML += textdocelowy.charAt(i);
//     i++;
//     setTimeout(typeWriter, speed);
//   }
// }

//   function fallbackCopyTextToClipboard(text) {
//     //animation
//     copytext.style.animationPlayState = "running";
    
//     //functionality
//   var textArea = document.createElement("textarea");
//   textArea.value = text;
  
//   // Avoid scrolling to bottom
//   textArea.style.top = "0";
//   textArea.style.left = "0";
//   textArea.style.position = "fixed";

//   document.body.appendChild(textArea);
//   textArea.focus();
//   textArea.select();

//   try {
//     document.execCommand('copy');
//   } catch (err) {
//     console.error("Nie udało się skopiować do schowka.")
//   }

//   document.body.removeChild(textArea);
// }
});
</script>

<template>
  <footer class="contact">
    <h1 class="contact_text">KONTAKT</h1>
    <div class="contact_blocks">
      <!-- <div class="contact_blocks_brand">
        <img src="../assets/icons/logo.png">
      </div> -->
      <div class="contact_blocks_buttons">
        <div class="contact_blocks_buttons_phone" id="phonenumber" onclick="window.location.href='tel:603893253'">
          <img src="../assets/icons/phone.png">
          <h2><span>661</span><span> 761 </span><span>799</span></h2>
          <div class="contact_blocks_buttons_phone_copy" id="copy">
            <h1><span id="copy_text">Skopiuj</span></h1>
          </div>
        </div>
        <div class="contact_blocks_buttons_fb" onclick="window.open('https://facebook.com/walkowiak.marek', '_blank')">
          <img src="../assets/icons/facebook.png">
          <h2><span>@wal</span><span>kowi</span><span>ak.m</span><span>arek</span></h2>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.contact{
  background: #E2F3F1;
  min-height: 350px;
  margin: 0;
  overflow: hidden;
  &_text{
    color: black;
    text-align: center;
    padding: 4vh 0vw 2vh 0vw;
  }
  &_blocks{
    display: flex;
    justify-content: center;
    //&_brand{
    //  position: absolute;
    //  height: 205px;
    //  padding: 0;
    //  margin: -65px 65vw 0px 0px;
    //  img{
    //    height: 205px;
    //  }
    //}
    &_buttons{
      display: flex;
      padding: 0;
      margin: 0;
      &_phone, &_fb{
        margin: 0;
        padding: 0;
        width: 130px;
        height: 130px;
        background: #58B9AF;
        border-radius: 25px;
        margin: 1vw;
        display: flex;
        position: relative;
        z-index: 2;
        transition: width 0.5s ease;
        img{
          height: 120px;
          margin: 5px;
          padding: 0;
        }
        h2{
          color: black;
          font-size: 43px;
          padding: 30px 0px;
          transform: scale(0.94);
          span{
            opacity: 0;
            filter: blur(4px);
          }
        }
      }
      &_phone:hover, &_fb:hover{
        background: #38A499;
      }
      &_phone_copy{
        background: #0b211f;
        position: absolute;
        height: 50px;
        width: 120px;
        border-radius: 0px 25px 25px 25px;
        top: 80px;
        right: 0px;
        opacity: 0;
        transition: top 0.5s ease, opacity 0.2s ease;
        //transition: opacity 0.1s ease;
        h1{
          color: #ebf6f5;
          margin: 0px 10px;
        }
      //  opacity: 0;
      //  h1{
      //    display: none;
      //  }
      }
    }
  }
}

@media only screen and (max-width: 700px){
  
}

@media only screen and (min-width: 701px){
  .contact_blocks_buttons{
    &_fb:hover{
      cursor: pointer;
      width: 540px;
      h2{
        animation: scale 0.5s forwards cubic-bezier(0.5, 1, 0.89, 1);
        span:nth-child(1){
          animation: fade-in 0.2s 0s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
        span:nth-child(2){
          animation: fade-in 0.2s 0.1s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
        span:nth-child(3){
          animation: fade-in 0.2s 0.2s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
        span:nth-child(4){
          animation: fade-in 0.2s 0.3s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
      }
    }
    &_phone:hover{
      width: 370px;
      .contact_blocks_buttons_phone_copy{
        top: 130px;
        opacity: 1;
      }
      h2{
        animation: scale 0.5s forwards cubic-bezier(0.5, 1, 0.89, 1);
        span:nth-child(1){
          animation: fade-in 0.2s 0s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
        span:nth-child(2){
          animation: fade-in 0.2s 0.1s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
        span:nth-child(3){
          animation: fade-in 0.2s 0.2s forwards cubic-bezier(0.11, 0, 0.5, 0);
        }
      }
    }
    &_phone_copy:hover{
      background: #11312e;
      cursor: pointer;
    }
  }
}

@keyframes scale {
  100% {
    transform: scale(1);
  }
}
@keyframes fade-in {
  100% {
    opacity: 1;
    filter: blur(0);
  }
}
</style>
