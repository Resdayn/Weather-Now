<template>
  <div>
    <h1>Weather Now</h1>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Audiowide&display=swap');
h1 {
  font-family: 'Audiowide', cursive;
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  font-size: 60px;
  padding: 2rem 0;
  color: #FCFEFC;
}

@media screen and (max-width: 480px) {
  h1 {
    font-size: 40px;
  }
}
</style>
