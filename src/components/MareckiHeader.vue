<template>
  <header>
    <h1 id="tytuł">Marecki</h1>
    <h3>Wykończenia wnętrz</h3>
  </header>
</template>

<style scoped lang="scss">
header{
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100px;
  transition: height 0.5s ease;
  background-color: #205F59;
  z-index: 9999;
  h1{
    font-size: 40px;
    transition: font-size 0.5s ease;
    margin-left: 1vw;
  }
  h3{
    font-size: 15px;
    transition: font-size 0.5s ease;
    margin-left: 1vw;
  }
}

@media only screen and (max-width: 700px){
  header{
    height: 70px;
    h1{
      font-size: 25px;
    }
    h3{
      font-size: 10px;
    }
  }
}

</style>
