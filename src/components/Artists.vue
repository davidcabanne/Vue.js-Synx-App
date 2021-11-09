<template :key="componentKey">
  <div class="bloc__container flex__ctr bloc__marginLrg">
    <div class="bloc__wrapper artist__section">
      <!-- artist section starts -->
      <div
        v-for="artist in artists"
        :key="artist.id"
        class="loading__animation"
      >
        <div class="artist__container flex__ctr">
          <div class="artist__overlay"></div>
          <div class="artist__name">{{ artist.artistName }}</div>
          <img :src="artist.picture" class="artist__picture" />
        </div>
      </div>
      <!-- artist section ends -->
    </div>
  </div>
</template>

<script>
export default {
  name: "Artists",
  data() {
    return {
      artists: {
        artistOne: {
          artistName: "Brian Eno",
          picture:
            "https://lecanalauditif.ca/wp-content/uploads/2018/01/brian-eno.jpeg",
        },
        artistTwo: {
          artistName: "Philip Glass",
          picture:
            "https://www.musicologie.org/Biographies/g/i/glass_philip.jpg",
        },
        artistThree: {
          artistName: "Huerco S",
          picture:
            "https://www.benzinemag.net/wp-content/uploads/2016/06/Huerco-S-2.jpg",
        },
        artistFour: {
          artistName: "Project Pablo",
          picture:
            "https://www.stampthewax.com/wp-content/uploads/2020/05/Webp.net-resizeimage-2020-05-06T152456.418-600x400.jpg",
        },
        artistFive: {
          artistName: "Felicia Atkinson",
          picture:
            "https://static.qobuz.com/images/artists/covers/medium/987996e16ff80d53c765828234038af6.jpg",
        },
      },
    };
  },
  methods: {},
  mounted() {},
};
</script>

<style scoped lang="scss">
.loading__animation {
  opacity: 0;
  animation: blendIn 1s forwards cubic-bezier(0.77, 0, 0.18, 1);
  animation-delay: 0.5s;
  @for $i from 1 through 10 {
    &:nth-child(#{$i}) {
      animation-delay: $i * 0.05s;
    }
  }
}
@keyframes blendIn {
  0% {
    // transform: translateY(30px);
    opacity: 0;
  }
  100% {
    // transform: translateY(0px);
    opacity: 1;
  }
}

.artist__section {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
  grid-gap: 15px;
}

.artist__container {
  position: relative;
  max-width: calc(1240px / 5);
  min-width: 170px;
  height: 150px;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 5px 5px 16px 5px rgba(0, 0, 0, 0.1);
}

.artist__overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--greenPrimary);
  cursor: pointer;
  opacity: 0.35;
  transition: opacity 0.35s ease-in-out;
}

.artist__name {
  position: absolute;
  bottom: 0;
  left: 0;
  margin: 0 0 15px 15px;
}

.artist__picture {
  width: 100%;
  height: 150px;
  object-fit: cover;
  transition: transform 0.25s ease-in-out;
  z-index: -1;
}

.artist__container:hover > .artist__overlay {
  opacity: 0.5;
}
.artist__container:hover > .artist__picture {
  transform: scale(1.1);
}
</style>
