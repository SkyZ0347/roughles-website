<script setup>
import { ref } from 'vue';

const itemName = ref('');
const skyzName = ref('');
const frytName = ref('');
// const strzaName = ref('');

itemName.value = 'RoughlesBH @gmail.com';
skyzName.value = 'skyz03';
frytName.value = 'xfryertuck';
// strzaName.value = 'strzalsonik';

function copyMail(){
  const mailItem = document.querySelector('.contact_block_mail');
  mailItem.classList.remove('wigglemail');
  mailItem.classList.add('wigglemail');

  skyzName.value = 'skyz03';
  frytName.value = 'xfryertuck';
  // strzaName.value = 'strzalsonik';

  itemName.value = "Skopiowano";
  setTimeout(() => {
    itemName.value = 'RoughlesBH @gmail.com';
    mailItem.classList.remove('wigglemail');
  }, 800);
}

function copyDiscord(className){
  document.querySelector(`.skyz03`).classList.remove('wiggledc');
  document.querySelector(`.xfryertuck`).classList.remove('wiggledc');
  // document.querySelector(`.strzalsonik`).classList.remove('wiggledc');

  const item = document.querySelector(`.${className}`);
  item.classList.remove('wiggledc');
  item.classList.add('wiggledc');

  itemName.value = 'RoughlesBH @gmail.com';
  skyzName.value = 'skyz03';
  frytName.value = 'xfryertuck';
  // strzaName.value = 'strzalsonik';

  switch (className) {
    case 'skyz03': 
      skyzName.value = "Skopiowano";
      break;
    case 'xfryertuck': 
      frytName.value = "Skopiowano";
      break;
    // case 'strzalsonik':
    //   strzaName.value = "Skopiowano";
    //   break;
  }

  setTimeout(() => {
    item.classList.remove('wiggledc');
    skyzName.value = 'skyz03';
    frytName.value = 'xfryertuck';
    // strzaName.value = 'strzalsonik';
  }, 800);
}

</script>

<template>
  <footer class="contact">
    <h1 class="contact_text">KONTAKT</h1>
    <div class="contact_block">
      <div class="contact_block_discord">
        <h2 class="copydiscord skyz03" @click="copyDiscord('skyz03')"><font-awesome-icon class="discord" icon="fa-brands fa-discord" /> {{ skyzName }}</h2>
        <h2 class="copydiscord xfryertuck" @click="copyDiscord('xfryertuck')"><font-awesome-icon class="discord" icon="fa-brands fa-discord" /> {{ frytName }}</h2>
        <!-- <h2 class="copydiscord strzalsonik" @click="copyDiscord('strzalsonik')"><font-awesome-icon class="discord" icon="fa-brands fa-discord" /> {{ strzaName }}</h2> -->
      </div>
      <div class="contact_block_line"></div>
      <div class="contact_block_mail">
        <h2 class="copymail" @click="copyMail()"><font-awesome-icon class="mail" icon="fa-solid fa-envelope" /> {{ itemName }}</h2>
      </div>
    </div>
  </footer>
</template>

<style scoped lang="scss">
.contact {
  background: #0a0b13;
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  width: 100vw;
  justify-content: center;

  h1{
    font-size: 2em;
  }

  &_text {
    color: #e8e8e8;
    text-align: center;
    padding: 2rem 0 1.5rem 0;
  }

  &_block {
    color: #e8e8e8;
    display: flex;
    justify-content: center;
    text-align: center;
    align-content: center;
    position: relative;

    &_discord,
    &_mail {
      //flex: 1; /* Allow the blocks to take equal space */
      display: flex;
      flex-direction: column;
      align-items: center; /* Center items vertically */
      transform: translateX(1.5rem);
      margin: 0 5.5rem 2.5rem 0;
      text-align: center;
      justify-content: center;
      h2{
        //white-space: nowrap;
        font-size: 1.1em;
      }
      .copydiscord{
        &:hover{
          cursor: pointer;
        }
      }
    }
    &_mail{
      width: 2rem;
      .copymail{
        &:hover{
          cursor: pointer;
        }
      }
    }
    .wigglemail{
      animation: wigglemail .5s forwards;
    }

    .wiggledc{
      animation: wiggledc .5s forwards;
    }

    &_line {
      width: 0.3rem;
      height: 4.6rem;
      background: #e8e8e8;
      margin: 0;
      position: absolute;
    }

    .discord {
      color: #6885d2;
    }

    .mail{
      color: #f7695c;
    }

    h2 {
      color: #e8e8e8;
    }
  }
}

@keyframes wigglemail {
    0% { transform: translateX(1.5rem) rotate(10deg); }
   25% { transform: translateX(1.5rem) rotate(-7deg); }
   50% { transform: translateX(1.5rem) rotate(5deg); }
   75% { transform: translateX(1.5rem) rotate(-3deg); }
  100% { transform: translateX(1.5rem) rotate(0deg); }
}

@keyframes wiggledc {
  0% { transform: rotate(10deg); }
 25% { transform: rotate(-7deg); }
 50% { transform: rotate(5deg); }
 75% { transform: rotate(-3deg); }
100% { transform: rotate(0deg); }
}

@media only screen and (max-width: 700px) {
  /* Add any responsive styling if needed */
}
</style>

