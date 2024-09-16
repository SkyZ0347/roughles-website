<script>
export default {
  props: {
    scrollTop: {
      type: Number,
      required: true
    }
  },
  // methods: {
  //   handleMouseMove(event) {
  //     const imageContainer = this.$refs.imageContainer;
  //     const rect = imageContainer.getBoundingClientRect();
  //     const x = event.clientX - rect.left;
  //     const y = event.clientY - rect.top;

  //     const canvas = document.createElement('canvas');
  //     const ctx = canvas.getContext('2d');
  //     const image = document.querySelector('#Nagrody');

  //     // Ensure image is loaded
  //     if (image.complete) {
  //       canvas.width = image.width;
  //       canvas.height = image.height;
  //       ctx.drawImage(image, 0, 0);

  //       const pixel = ctx.getImageData(x, y, 1, 1).data;
  //       const alpha = pixel[3];

  //       // Change cursor based on alpha value
  //       if (alpha > 0) {
  //         imageContainer.style.cursor = 'pointer';
  //       } else {
  //         imageContainer.style.cursor = 'default';
  //       }
  //     }
  //   },
  //   handleImageClick(event) {
  //     const imageContainer = this.$refs.imageContainer;
  //     const rect = imageContainer.getBoundingClientRect();
  //     const x = event.clientX - rect.left;
  //     const y = event.clientY - rect.top;

  //     const canvas = document.createElement('canvas');
  //     const ctx = canvas.getContext('2d');
  //     const image = document.querySelector('#Nagrody');

  //     // Ensure image is loaded
  //     if (image.complete) {
  //       canvas.width = image.width;
  //       canvas.height = image.height;
  //       ctx.drawImage(image, 0, 0);

  //       const pixel = ctx.getImageData(x, y, 1, 1).data;
  //       const alpha = pixel[3];

  //       if (alpha > 0) {
  //         this.triggerLoteriaTransition();
  //       }
  //     }
  //   },
  //   triggerLoteriaTransition() {
  //     const rewardsOverlay = document.querySelector('.rewards-overlay');

  //     rewardsOverlay.style.left = '-10%';
  //   }
  // },
  // mounted() {
  //   const imageContainer = this.$refs.imageContainer;
  //   imageContainer.addEventListener('click', this.handleImageClick);
  //   imageContainer.addEventListener('mousemove', this.handleMouseMove);
  // },
  // beforeUnmount() {
  //   const imageContainer = this.$refs.imageContainer;
  //   imageContainer.removeEventListener('click', this.handleImageClick);
  //   imageContainer.removeEventListener('mousemove', this.handleMouseMove);
  // }
};
</script>

<template>
  <!-- <div class="rewards-overlay" ref="rewardsOverlay"></div> -->
  <div ref="imageContainer" class="content">
    <div class="content_block">
      <img id="Nagrody" src="../assets/photos/Nagrody.webp">
      <h1>Offline</h1>
    </div>
  </div>
</template>

<style scoped lang="scss">
.rewards-overlay{
  position: fixed;
  top: 0;
  left: 115%;
  width: 120vw;
  height: 100vh;
  background: #181a32;
  z-index: 1000;
  transform: skew(-15deg);
  display: flex;
  justify-content: center;
  align-items: flex-end;
  overflow: hidden;
  transition: left 1.5s ease-out;

  &:before{
    content: "";
    position: absolute;
    left: 1%;
    width: 120vw;
    height: 100vh;
    background: #0a0b13;
  }
}

.content{
  //width: 100%;
  align-items: center;
  justify-content: center;
  //background: rgba($color: #000000, $alpha: 0.4);
  margin-bottom: 30px;
  &_block{
    width: 100%;
    //width: 93vw;
    //max-width: 1200px;
    //max-height: 724px;
    margin: 30px auto 0px auto;
    #Nagrody{
      width: 100%;
      filter: blur(0.2rem) grayscale(1);
      &::before {
        content: '';
        width: 100%;
        height: 100%;
        z-index: 1;
        background-color: rgba(255,255,255,0.1);
        transition: all 0.3s;
      }
      &::after {
        content: '';
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
    h1{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translateX(-50%);
      font-size: 3em;
      color: white;
      filter:drop-shadow(0.2rem 0.2rem 0.2rem black);
    }
  }
}

</style>