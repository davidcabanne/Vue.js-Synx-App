<template>
  <div class="bloc__container flex__ctr hero__section">
    <div class="bloc__wrapper flex__ctr">
      <div class="hero__punchline">
        The right music for your product.
        <div class="hero__punchline--glow">
          The right music for your product.
        </div>
      </div>
      <div class="hero__text">
        Discover and purchase original tracks from real artists. <br />
        Start your free trial now and find what your music has been missing.
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style scoped lang="scss">
.hero__section {
  min-height: 50vh;
}

.bloc__wrapper {
  flex-direction: column;
  align-items: flex-start;
}

.hero__punchline,
.hero__text {
  width: 90vw;
  max-width: 1240px;
}

.hero__punchline {
  position: relative;
  font-size: clamp(25px, 8vw, 48.83px);
  font-weight: 700;
  margin-bottom: var(--spaceMed);
}

.hero__punchline--glow {
  position: absolute;
  top: 0;
  left: 0;
  font-size: clamp(25px, 8vw, 48.83px);
  font-weight: 700;
  filter: blur(4px);
  animation: blur_animation 10s ease-in-out infinite;
}

@keyframes blur_animation {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 0;
  }
}

.hero__text {
  line-height: 1.5;
}
</style>
