<template>
  <div class="background__stain"></div>
  <div class="background__fixed"></div>
  <!-- <div class="background__container">
    <img class="background__img" src="../assets/backgroundtexture.png" />
  </div> -->
</template>

<script>
export default {
  name: "Background",
};
</script>

<style scoped>
.background__fixed {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: linear-gradient(
    75deg,
    var(--darker),
    var(--darker),
    var(--greenDark)
  );
  z-index: -1;
}

.background__container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.background__img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  background-repeat: repeat;
  opacity: 0.4;
}
</style>
