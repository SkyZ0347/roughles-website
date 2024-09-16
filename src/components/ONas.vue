<script>
export default {
  setup() {
    const joinDiscord = () => {
      window.open('https://discord.com/invite/9SBKvKVVVw', '_blank');
    };
    return {
      joinDiscord
    };
  }
};
</script>

<template>
  <div class="content">
    <div class="content_block">
      <div class="content_block_left">
        <p>Jesteśmy zgraną i dynamiczną społecznością graczy, skupionych wokół gry Brawlhalla, 
          jednego z czołowych tytułów gatunku platform fighter. Naszym celem jest nieustanne 
          doskonalenie umiejętności naszych członków oraz reprezentowanie naszej organizacji na 
          najwyższym poziomie podczas różnorodnych wydarzeń, w tym turniejów. 
          Wierzymy w siłę wspólnej pasji i zaangażowania, co pozwala nam budować trwałe 
          relacje i wspierać się nawzajem w udoskonalaniu swoich umiejętności.</p>
        <p>Dołącz do nas, aby razem 
          podnosić poprzeczkę i zdobywać nowe szczyty na scenie Brawlhalli!</p>
      </div>
      <div class="content_block_right">
        <h2>Nasza organizacja poszukuje graczy, 
          o podobnym lub wyższym poziomie umiejętności, 
          jaki prezentują nasi gracze, zachęcamy wszystkich 
          do zgłoszenia się na naszym Discordzie w celu weryfikacji.</h2>
        <h1 @click="joinDiscord"><font-awesome-icon icon="fa-brands fa-discord" /> Join</h1>
        <div class="content_block_right_image">
          <img src="/src/assets/photos/BHRenders/SkyZ_1.avif">
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.content {
  &_block {
    display: flex;
    flex-wrap: wrap;
    margin-top: 1rem;
    width: 100%;
    //margin-bottom: 30px;
    //background: rgba(0, 0, 0, 0.4);
    position: relative;
    overflow: visible;

    &_left {
      width: 70%;
      background: #0a0b13;
      z-index: 30;
      clip-path: polygon(0 0, 150% 0, 150% 150%, 25% 150%, 0 90%);
      transition: clip-path 0.5s ease;
      padding: 1.2% 2.4%;
      p {
        font-size: 1.2em;
        margin: 1rem;
        color: white;
        text-align: justify;
        transition: height .2s ease, font-size .2s ease;
      }
      p + p {
        padding: 2% 15% 0% 0%;
        margin-bottom: 1rem;
      }
      &_line{
        position: absolute;
        bottom: 1rem;
        right: 0;
        height: 7px;
        width: 120px;
        background: #e5cc70;
      }
    }

    &_right {
      width: 30%;
      padding: 0;
      background: #e8e8e8;
      z-index: 30;
      justify-content: center;
      text-align: center;
      overflow: visible;
      position: relative;
      z-index: 40;
      clip-path: polygon(0 -90%, 150% 60%, 550% 100%, 0% 100%, 0 90%);
      transition: clip-path 0.5s ease;
      h2 {
        margin: 2rem 2.5rem;
        height: 13.4vw;
        font-size: 1.1em;
        color: #0a0b13;
        text-align: justify;
      }
      h1 {
        position: absolute;
        left: 50%;
        bottom: 14%;
        transform: translateX(-50%);
        padding: 0.5rem 1rem;
        font-size: 2em;
        font-family: 'BHFont';
        font-weight: 800;
        color: #e4e4e4;
        background-color: #0a0b13;
        border-radius: 1rem;
        transition: all 0.5s;
        animation: none;
        white-space: nowrap;
        &::before {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          z-index: 1;
          background-color: rgba(255,255,255,0.1);
          transition: all 0.3s;
        }
        &::after {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          z-index: 1;
          opacity: 0;
          transition: all 0.3s;
          border: 1px solid #0a0b13;
          transform: scale(1.2,1.2);
        }
        &:hover {
          cursor: pointer;
          border-radius: 0rem;
          &::before {
            opacity: 0 ;
            transform: scale(0.5,0.5);
          }
          &::after {
            opacity: 1;
            transform: scale(1,1);
          }
        }
      }
      &_line{
        position: absolute;
        bottom: 20px;
        left: 0;
        height: 7px;
        width: 60px;
        background: #e5cc70;
      }
      &_image {
        position: absolute;
        bottom: 0;
        right: -5vw;
        height: 50%;
        z-index: 60;
        overflow: visible;
        transition: right .2s ease;
        img {
          overflow: visible;
          transform: scaleX(-1);
          height: 98%;
          z-index: 70;
          filter: drop-shadow(0.2vw 0.4vw 0 #e8e8e8) 
                  drop-shadow(-0.4vw -0.2vw 0 #e8e8e8);
        }
      }
    }
  }

  &:after {
    content: '';
    display: table;
    clear: both;
  }
}

@media only screen and (max-width: 1440px) {
  .content {
    &_block {
      &_left {
        p {
          font-size: 1em;
        }
      }
      &_right {
        h2 {
          margin: 1.8rem 2rem;
          font-size: 0.9em;
        }
        h1 {
          font-size: 1.3em;
        }
        &_image{
          right: -4.5em;
        }
      }
    }
  }
}

@media only screen and (max-width: 1024px) {
  .content {
    &_block {
      &_left {
        p {
          font-size: 0.7em;
        }
      }
      &_right {
        h2 {
          margin: 1.8rem 2rem;
          font-size: 0.6em;
        }
        h1 {
          font-size: 1em;
        }
        &_image{
          right: -3.2rem;
        }
      }
    }
  }
}

@media only screen and (max-width: 800px) {
  .content {
    display: inline-block;
    &_block {
      &_left{
        width: 100%;
        padding: 3vw;
        clip-path: polygon(0 0, 93% 0%, 180% 150%, 0% 100%, 0 100%);
        p {
          font-size: 2vw;
        }
      }
      &_right {
        width: 100%;
        clip-path: polygon(0% 0%, 150% 0%, 150% 100%, 7% 100%, 0% 83%);
        h2 {
          margin: 1.2rem 1rem 6rem 1rem;
          padding: 2.5vw;
          font-size: 2.3vw;
        }
        h1 {
          bottom: 5%;
          font-size: 5vw;
          padding: 0.7rem 1rem;
        }
        &_image{
          right: -2.7rem;
        }
      }
    }
  }
}

</style>