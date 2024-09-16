<script>
import AuthMenu from '../components/AuthMenu.vue';
import axios from 'axios';
import eventBus from '../../eventBus';

import { useRouter } from "vue-router";

let discord_id = 0;

export default {
  name: 'PageHeader',
  components: {
    AuthMenu
  },
  props: {
    navItems: Array,
    style: Object,
    loteria: String,
    discord_id: Number
  },
  data() {
    return {
      owned_chests: [],
      brawler: null,
      elite: null,
      legend: null,
      chest_codes: [],
      chest: null,
      redeemCode: '',
      isInvalidHidden: true,
      isActive: false,
      isTransitioning: false,
      isHamburgerOpen: false,
      isMobile: false
    }
  },
  setup() {
    const router = useRouter();

    const goHome = () => {
      router.push('/');
    };

    return {
      goHome
    };
  },
  computed: {
    isLoteriaPage() {
      return this.$route.path === '/Loteria';
    },
    chestHowToOpacity() {
      return this.isActive ? 1 : 0;
    }
  },
  methods: {
    // Function to handle code submission
    async handleSubmit() {
      try {
        // Fetch all chest codes
        const codeResponse = await axios.get('http://localhost:3030/chest_codes');
        const codes = codeResponse.data;

        // Find the code in chest_codes
        const codeEntry = codes.find(code => code.code === this.redeemCode);

        if (codeEntry && discord_id != 0) {
          const codeId = codeEntry.id;

          //Update the chest_codes on the server
          await axios.delete(`http://localhost:3030/chest_codes/${codeId}`, {
            headers: {
              'Content-Type': 'application/json'
            }
          })
            .catch((error) => {
              console.error(error);
            });
          const chestsResponse = await axios.get(`http://localhost:3030/owned_chests?discord_id=${discord_id}`);
          const ownedChests = chestsResponse.data;
          const updateField = codeEntry.chest;

          if (ownedChests.length > 0) {

            const chestToUpdate = ownedChests[0];
            const updatedChest = {
              ...chestToUpdate,
              [updateField]: (chestToUpdate[updateField] || 0) + 1
            };


            // Send update request to json-server
            await axios.put(`http://localhost:3030/owned_chests/${ownedChests[0].id}`, updatedChest, {
              headers: {
                'Content-Type': 'application/json'
              }
            })
              .catch((error) => {
                console.error(error);
              });
            // Update local state
            this.brawler = updatedChest.brawler;
            this.elite = updatedChest.elite;
            this.legend = updatedChest.legend;

            const message = document.querySelector('.message');
            message.style.color = 'rgb(25, 255, 25)'
            message.textContent = 'Kod odebrany pomyślnie!';
            this.isInvalidHidden = false;

          } else {
            const newChest = {
              discord_id: discord_id,
              brawler: 0,
              elite: 0,
              legend: 0
            };

            newChest[updateField] = 1;

            await axios.post('http://localhost:3030/owned_chests', newChest, {
              headers: {
                'Content-Type': 'application/json'
              }
            });

            // Update local state
            this.brawler = updateField === 'brawler' ? 1 : 0;
            this.elite = updateField === 'elite' ? 1 : 0;
            this.legend = updateField === 'legend' ? 1 : 0;

            const message = document.querySelector('.message');
            message.style.color = 'rgb(25, 255, 25)'
            message.textContent = 'Kod odebrany pomyślnie!';
            this.isInvalidHidden = false;
          }
        } else {
          if (discord_id == 0) {
            const message = document.querySelector('.message');
            message.style.color = 'rgb(255, 25, 25)';
            message.textContent = 'Musisz być zalogowany na stronie!';
            this.isInvalidHidden = false;
          } else {
            const message = document.querySelector('.message');
            message.style.color = 'rgb(255, 25, 25)';
            message.textContent = 'Kod jest niepoprawny!';
            this.isInvalidHidden = false;
          }
        }
      } catch (error) {
        console.error('Error handling redemption:', error);
      }
    },
    toggleClass() {
      this.isActive = !this.isActive;
      if (this.isActive) {
        this.isTransitioning = false;
      } else {
        this.isTransitioning = true;
        setTimeout(() => {
          this.isTransitioning = false;
        }, 500); // Match this duration with your CSS transition duration
      }
    },
    openHamburger() {
      const mmButton = document.querySelector('.mm');
      const navLeft = document.querySelector('.nav_left');

      const applyTransition = () => {
        navLeft.style.transition = 'left 0.5s';
      };

      const removeTransition = () => {
        navLeft.style.transition = 'none';
      };

      if (mmButton.classList.contains('opened')) {
        mmButton.classList.remove('opened');
        void mmButton.offsetWidth;
        mmButton.classList.add('closing');

        applyTransition();
        navLeft.style.left = '-50vw';

        this.isHamburgerOpen = false;
        setTimeout(() => {
          removeTransition();
          mmButton.classList.remove('closing');
        }, 500);

      } else {
        mmButton.classList.add('opened');

        applyTransition();
        navLeft.style.left = '0vw';

        this.isHamburgerOpen = true;
        setTimeout(() => {
          removeTransition();
        }, 500);
      }
    },
    handleClickOutside(event) {
      const chestCounterDiv = document.querySelector('.chest_counter');
      const chestHowToDiv = document.querySelector('.chestsHowTo');

      if (
        (chestCounterDiv && !chestCounterDiv.contains(event.target)) &&
        (chestHowToDiv && !chestHowToDiv.contains(event.target))
      ) {
        this.isActive = false;
      }

      const headerDiv = document.querySelector('header');
      const navleftDiv = document.querySelector('.nav_left');

      if (
        (headerDiv && !headerDiv.contains(event.target)) &&
        (navleftDiv && !navleftDiv.contains(event.target)) &&
        this.isHamburgerOpen
      ) {
        this.openHamburger();
      }

    },
    toggleInvalidVisibility(isHidden) {
      this.isInvalidHidden = isHidden;
    },
    handleTransitionEnd() {
      if (!this.isActive) {
        this.isTransitioning = false;
      }
    },
    handleEnterPress(event) {
      if (event.key === "Enter") {
        event.preventDefault();
        document.querySelector('.submit-btn').click();
      }
    },
    getPlayersChestCount() {
      if (discord_id != 0) {
        fetch(`http://localhost:3030/owned_chests?discord_id=${discord_id}`)
        .then(res => res.json())
        .then(data => {
          if (data.length > 0) {
            const chestData = data[0];
            this.brawler = chestData.brawler;
            this.elite = chestData.elite;
            this.legend = chestData.legend;
          }
        })
        .catch(err => console.log(err.message));
      }
    },
    updateOnResize() {
      const navLeft = document.querySelector('.nav_left');
      const mobileMenu = document.querySelector('.mm');

      if (window.innerWidth > 800) {
        navLeft.style.left = '0vw';
        navLeft.style.transition = 'none';
        mobileMenu.classList.remove('opened');
        this.isMobile = false;
      }
      else {
        this.isMobile = true;
        if (mobileMenu) {
          if (!mobileMenu.classList.contains('opened')) {
            navLeft.style.left = '-50vw';
            navLeft.style.transition = 'none';
          }
        }
      }
    }
  },
  mounted() {
    this.getPlayersChestCount();
    this.updateOnResize();

    eventBus.on('updateDiscordID', e => {
      discord_id = e.id;
    })

    eventBus.on('updateChestCount', this.getPlayersChestCount())

    window.addEventListener('resize', this.updateOnResize);

    document.addEventListener('click', this.handleClickOutside);
    const chestHowToElement = document.querySelector('.chestsHowTo');
    if (chestHowToElement) {
      chestHowToElement.addEventListener('transitionend', this.handleTransitionEnd);
    }

    var input = document.getElementById("textInput");
    input.addEventListener("keypress", this.handleEnterPress);
  },
  unmounted() {
    document.removeEventListener('click', this.handleClickOutside);
    window.removeEventListener('resize', this.updateOnResize);
    const chestHowToElement = document.querySelector('.chestsHowTo');
    if (chestHowToElement) {
      chestHowToElement.removeEventListener('transitionend', this.handleTransitionEnd);
    }

    var input = document.getElementById("textInput");
    input.removeEventListener("keypress", this.handleEnterPress);
  },
};


</script>


<template>
  <header>
    <button aria-label="Mobile Menu" class="mm" @click="openHamburger()">
      <span class="mms"></span>
    </button>
    <img class="logo" src="../assets/icons/Roughles.png" @click="goHome" alt="Roughles">
    <div class="nav_left">
      <h2 v-for="(item, index) in navItems" v-bind="$attrs" :key="index" @click="item.action">
        {{ item.label }}
      </h2>
    </div>
    <div class="nav_right">
      <h3 v-if="isLoteriaPage && !isMobile" class="questionmark" @click.stop="toggleClass()">?</h3>
      <div v-if="isLoteriaPage && !isMobile" class="chest_counter">
        <div class="chest">
          <img src="../assets/Loteria/Chest1.avif" alt="Brawler">
          <h3 class="owned_brawlers"> {{ brawler }}</h3>
        </div>
        <div class="chest">
          <img src="../assets/Loteria/Chest2.avif" alt="Elite">
          <h3 class="owned_elites">{{ elite }}</h3>
        </div>
        <div class="chest">
          <img src="../assets/Loteria/Chest3.avif" alt="Legend">
          <h3 class="owned_legends">{{ legend }}</h3>
        </div>
      </div>
      <!-- <AuthMenu /> -->
    </div>
  </header>
  <div class="chestsHowTo" :class="{ 'active': isActive, 'hidden': !isActive && isTransitioning }"
    :style="{ opacity: chestHowToOpacity }" @click.stop>
    <h2>Jak zdobyć skrzynki?</h2>
    <p>Skrzynki można zdobyć biorąc udział w aktywnościach organizowanych przez Roughles,
      są to przykładowo konkursy, turnieje czy wydarzenia na discordzie.</p>
    <p>Oprócz tego skrzynkami można się wymieniać między sobą, w oknie otwarcia skrzynki znajduje się opcja
      <i>"Przekaż"</i>,
      która usuwa skrzynkę z konta i generuje kod do jej odebrania przez inną osobę.
    </p>
    <label class="redeem_label" for="textInput">Tutaj możesz odebrać skrzynkę od znajomego</label>
    <div class="redeemCode">
      <input type="text" id="textInput" class="input-box" placeholder="Podaj kod.." v-model="redeemCode"
        autocomplete="off" @focus="toggleInvalidVisibility(true)">
      <button class="submit-btn" @click="handleSubmit()">Wyślij</button>
    </div>
    <label class="message" v-bind:class="{ 'visible': !isInvalidHidden }">Kod jest niepoprawny!</label>
  </div>
</template>

<style scoped lang="scss">
header {
  position: fixed;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  background-color: #0a0b13;
  z-index: 9999;

  .logo {
    margin: 0.2rem 2.3rem;
    width: 4rem;
    transition: margin 0.4s ease;
    cursor: pointer;
  }

  .nav_left {
    position: relative;
    display: flex;
    width: auto;
    height: auto;
    top: 0;
    left: 0;
    transition: none;
    padding-left: 0;
    align-items: center;
    flex-grow: 1;
    overflow: hidden;

    h2 {
      white-space: unset;
    }
  }

  .nav_right {
    display: flex;
    align-items: center;
    justify-content: center;

    .questionmark {
      text-align: center;
      font-size: 30px;
      margin: 5px;
      background: none;
      backdrop-filter: none;
      color: white;

      &:hover {
        cursor: pointer;
      }
    }

    .chest_counter {
      display: flex;
      height: 100%;

      .chest {
        justify-content: center;
        align-items: center;
        align-content: center;
        text-align: center;

        img {
          display: block;
          height: 40px;
          margin: 3px 5px;
        }

        h3 {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          color: white;
          font-size: 18px;
          text-shadow:
            0 0 5px #000,
            0 0 8px #000,
            0 0 10px #000;
        }
      }
    }
  }
}

.chestsHowTo {
  position: absolute;
  top: 55%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 9999;
  border-radius: 5%;
  background: radial-gradient(hsl(0 0% 5% / 0.5), hsl(0 0% 5% / 0.5), hsl(0 0% 5% / 0.35), hsl(0 0% 5% / 0));
  backdrop-filter: blur(15px);
  transition: opacity 0.5s ease-out, visibility 0s ease 0.5s, top 0.5s ease-out;
  opacity: 0;
  visibility: hidden;
  pointer-events: none;

  h2 {
    text-align: center;
    font-size: 2vw;
    background: none;
    backdrop-filter: none;
    color: white;
    margin: 5% 0 0 0;
  }

  p {
    font-size: 1.2vw;
    margin: 5% 10% 0% 10%;
    color: white;
  }

  .redeem_label {
    text-align: center;
    color: white;
    font-size: 0.9vw;
    margin: 3% auto 0% auto;
    width: 100%;
  }

  .redeemCode {
    text-align: center;
    margin-bottom: 3%;

    input {
      border-radius: 3vw 0vw 0vw 3vw;
      background: hsl(0 0% 5% / 0.3);
      border: none;
      padding: 0.6vw 1.1vw;
      width: 14.4vw;
      font-size: 1vw;
      border: none;
      color: rgb(227, 227, 227);

      &:focus {
        outline: none;
      }

      &::placeholder {
        border: none;
        color: rgb(227, 227, 227);
      }
    }

    button {
      border-radius: 0vw 3vw 3vw 0vw;
      background: hsl(0 0% 5% / 0.3);
      border: none;
      font-size: 1vw;
      padding: 0.6vw 1.3vw;
      color: white;

      &:focus {
        outline: none;
      }

      &:hover {
        cursor: pointer;
      }
    }
  }

  .message {
    text-align: center;
    color: rgb(255, 25, 25);
    font-size: 1vw;
    margin: 3% auto 4% auto;
    width: 100%;
    visibility: hidden;
    transition: visibility 0.3s ease-in-out;
  }

  .invalid_code.visible {
    visibility: visible !important;
  }
}

.chestsHowTo.active {
  top: 50% !important;
  opacity: 1 !important;
  pointer-events: auto !important;
  visibility: visible;
  transition: opacity 0.5s ease-out, visibility 0s ease 0s, top 0.5s ease-out;
}

.chestsHowTo.hidden {
  visibility: hidden;
  transition: opacity 0.5s ease, visibility 0s 0.5s;
}

header {
  h2 {
    padding: 2rem 1rem;
    font-size: 1em;
    margin: 0;
    transition: padding 0.4s ease;
    color: #e8e8e8;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  h2:hover {
    color: #0a0b13;
    background: #e8e8e8;
    transition: color 0.2s ease, background 0.2s ease;
    cursor: pointer;
  }
}

.mm {
  visibility: hidden;
}

@media only screen and (max-width: 1440px) {
  header {
    .nav_left {
      h2 {
        padding: 2rem 0.5rem;
      }
    }

    .logo {
      margin: 0.2rem 0.5rem;
    }
  }
}

@media only screen and (max-width: 800px) {
  header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100vw;
    background: #0a0b13;
    position: relative;

    .logo {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);

      &:active {
        filter: brightness(70%);
        transition: filter 0.5s;
      }
    }

    .nav_left {
      position: absolute;
      display: block;
      width: 50vw;
      height: 100vh;
      top: 5.4rem;
      left: -50vw;
      padding-left: 1rem;
      background: #e8e8e8;

      h2 {
        color: #0a0b13;
        padding: 1.5rem 0rem;
      }
    }

    .nav_right {
      margin-left: auto;

      h2 {
        &:active {
          background: red;
        }
      }
    }
  }

  .mm {
    visibility: visible;
    z-index: 9999;
    all: unset;
    width: 20px;
    height: 20px;
    padding: 10px;
    position: absolute;
    left: 1rem;

    .mms {
      left: 10px;
      position: absolute;
      width: 20px;
      height: 2px;
      background: #fff;
      pointer-events: none;
    }

    .mms::before {
      content: '';
      position: absolute;
      top: -7px;
      width: 20px;
      height: 2px;
      background: #fff;
      pointer-events: none;
    }

    .mms::after {
      content: '';
      position: absolute;
      top: 7px;
      width: 20px;
      height: 2px;
      background: #fff;
      pointer-events: none;
    }
  }

  .mm.opened .mms::before {
    animation: hamburger-top 0.5s forwards;
  }

  .mm.opened .mms::after {
    animation: hamburger-bottom 0.5s forwards;
  }

  .mm.opened .mms {
    animation: hamburger-middle 0.5s forwards;
  }

  .mm.closing .mms::before {
    animation: hamburger-top 0.5s reverse forwards;
  }

  .mm.closing .mms::after {
    animation: hamburger-bottom 0.5s reverse forwards;
  }

  .mm.closing .mms {
    animation: hamburger-middle 0.5s reverse forwards;
  }
}

@keyframes hamburger-top {

  0% {
    top: 7px;
  }

  50% {
    top: 0px;
    transform: rotate(0deg);
  }

  100% {
    top: 0px;
    transform: rotate(0deg);
  }
}

@keyframes hamburger-middle {

  0% {}

  50% {

    transform: rotate(0deg);
  }

  100% {

    transform: rotate(45deg);
  }
}

@keyframes hamburger-bottom {

  0% {
    top: -7px;
  }

  50% {
    top: 0px;
    transform: rotate(0deg);
  }

  100% {
    top: 0px;
    transform: rotate(-90deg);
  }
}
</style>
