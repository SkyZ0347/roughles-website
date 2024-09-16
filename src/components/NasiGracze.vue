<template>
  <div class="content">
    <div class="content_block">
      <div class="content_block_title">
        <h1>Ekipa Roughles</h1>
      </div>
      <div class="content_block_display">
        <div class="content_block_display_card" v-for="(character, index) in characters" :key="index">
          <img :src="getImage(character.image)" :alt="character.name">
          <h2>{{ character.name }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const characters = ref([
  { name: 'SkyZ', image: '../assets/BHCharacters/SkyZ.avif' },
  { name: 'Frytkownica', image: '../assets/BHCharacters/Frytkownica.avif' },
  { name: 'Strzałson', image: '../assets/BHCharacters/Strzałson.avif' },
  { name: 'Dejv', image: '../assets/BHCharacters/Dejv.avif' },
  { name: 'NayroD', image: '../assets/BHCharacters/NayroD.avif' },
  { name: 'Shogun', image: '../assets/BHCharacters/Shogun.avif' },
  { name: 'Sarcasm', image: '../assets/BHCharacters/Sarcasm.avif' },
  { name: 'VicE', image: '../assets/BHCharacters/VicE.avif' },
  { name: 'Tomii', image: '../assets/BHCharacters/Tomii.avif' },
  { name: 'Ryciu', image: '../assets/BHCharacters/Ryciu.avif' },
  { name: 'Kxcperek', image: '../assets/BHCharacters/Kxcperek.avif' },
  { name: 'Szvmskyy', image: '../assets/BHCharacters/Szvmskyy.avif' },
  { name: 'Roball', image: '../assets/BHCharacters/Roball.avif' },
  { name: 'Iruk', image: '../assets/BHCharacters/Iruk.avif' },
  { name: 'Nijo', image: '../assets/BHCharacters/Nijo.avif' },
  { name: 'Dodosu', image: '../assets/BHCharacters/Dodosu.avif' },
  { name: 'TieLikeFish', image: '../assets/BHCharacters/TieLikeFish.avif' },
  { name: 'Haizaki', image: '../assets/BHCharacters/Haizaki.avif' },
  { name: 'JOK3R', image: '../assets/BHCharacters/JOK3R.avif' },
  { name: 'BEPO', image: '../assets/BHCharacters/BEPO.avif' },
  { name: 'Dawidek', image: '../assets/BHCharacters/Inactive.avif' },
  { name: 'Ryszard Tragarz', image: '../assets/BHCharacters/RyszardTragarz.avif' },

  { name: 'SkyZ', image: '../assets/BHCharacters/SkyZ.avif' },
  { name: 'Frytkownica', image: '../assets/BHCharacters/Frytkownica.avif' },
  { name: 'Strzałson', image: '../assets/BHCharacters/Strzałson.avif' },
  { name: 'Dejv', image: '../assets/BHCharacters/Dejv.avif' },
  { name: 'NayroD', image: '../assets/BHCharacters/NayroD.avif' }
]);

const getImage = (image) => {
  return new URL(image, import.meta.url).href;
};
</script>

<style scoped lang="scss">
.content {
  width: 100%;
  align-items: center;
  justify-content: center;
  margin-bottom: 2rem;

  & .content_block {
    margin: 2rem auto;

    & .content_block_title {
      width: 100%;
      background: #e8e8e8;//#0a0b13;
      margin-bottom: 0.3rem;
      padding: 0.5rem 0;
      text-align: center;
      justify-content: center;
      align-items: center;
      h1{
        font-size: 1.5em;
        padding: 5rem auto;
        margin: 0;
        color: #0a0b13;//#e8e8e8;
      }
    }

    & .content_block_display {
      width: 100%;
      display: flex;
      overflow: hidden; /* Ensure the scrolling effect works */
      background: rgba(0, 0, 0, 0);
      margin-bottom: 0.5rem;

      & .content_block_display_card {
        flex: 0 0 auto; /* Ensure cards don't shrink */
        width: 19.68%;
        margin: 0px 0.4% 0px 0px;
        text-align: center;
        background: #0a0b13;
        animation: scroll 24s linear infinite;
        z-index: 100;

        img {
          width: 100%;
          display: block;
          margin-bottom: 0.5vw;
          z-index: 100;
        }

        h2 {
          color: #e8e8e8;
          font-size: 0.8rem;
        }
      }
    }
  }
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-102% * 22);
  }
}
</style>
