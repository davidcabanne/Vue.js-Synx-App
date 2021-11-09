<template>
  <div class="bloc__container flex__ctr bloc__marginLrg">
    <div class="bloc__wrapper artist__section">
      <!-- settings section starts -->
      <div class="mainContainer__grid">
        <Tracklist />
        <div class="playlistSettings__container">
          <Playlist />
          <div class="showTracklist__container">
            <div class="showTracklist__cta" @click="showSettings">
              <div
                class="showTracklist__title"
                :class="{
                  'showTracklist__title--isActive': showSettingsActive,
                }"
              >
                Show Tracklist Settings
                <transition name="glow">
                  <div
                    class="showTracklist__title--glow"
                    :class="{
                      'showTracklist__title--glowIn': showSettingsActive,
                      'showTracklist__title--glowOut': !showSettingsActive,
                    }"
                  >
                    Show Tracklist Settings
                  </div>
                </transition>
              </div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="3.0395mm"
                height="6.1238mm"
                viewBox="0 0 8.6159 17.3587"
                class="showTracklist__icon"
                :class="{ 'showTracklist__icon--isActive': showSettingsActive }"
              >
                <path
                  d="M.7687,0a.7467.7467,0,0,1,.53.22l6.52,6.52a2.7349,2.7349,0,0,1,0,3.86l-6.52,6.52A.75.75,0,0,1,.2013,16.0974q.018-.0194.0374-.0374l6.52-6.52a1.2354,1.2354,0,0,0,0-1.7393L.2387,1.28A.75.75,0,0,1,.7687,0Z"
                />
              </svg>
            </div>
            <transition name="fade">
              <div v-if="showSettingsActive">
                <Settings
                  v-for="settingsOpt in settingsOpts"
                  :key="settingsOpt.id"
                  :settingsOpt="settingsOpt"
                  class="settings__blendsIn--animation"
                />
              </div>
            </transition>
          </div>
        </div>
      </div>
      <!-- settings section ends -->
    </div>
  </div>
</template>

<script>
import Tracklist from "@/components/Tracklist";
import Playlist from "@/components/Playlist";
import Settings from "@/components/Settings";

export default {
  name: "MainContainer",
  components: {
    Tracklist,
    Playlist,
    Settings,
  },
  data() {
    return {
      showSettingsActive: false,
      settingsOpts: [
        {
          title: "Popularity",
          minValue: "Playing at bars",
          maxValue: "World Tour",
        },
        {
          title: "Energy",
          minValue: "Chill",
          maxValue: "Banger",
        },
        {
          title: "Vocals",
          minValue: "None",
          maxValue: "A Ton",
        },
        {
          title: "Tempo",
          minValue: "Slow",
          maxValue: "Fast",
        },
        {
          title: "Danceable",
          minValue: "Not at all",
          maxValue: "Boogie",
        },
        {
          title: "Acoustics",
          minValue: "All digital",
          maxValue: "All analog",
        },
      ],
    };
  },
  methods: {
    showSettings: function() {
      console.log("Toggle showSettings");
      this.showSettingsActive = !this.showSettingsActive;
    },
  },
};
</script>

<style scoped lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s cubic-bezier(0.86, 0, 0.07, 1);
}
.fade-enter-active {
  animation: fades_in 0.3s cubic-bezier(0.86, 0, 0.07, 1) forwards;
}

.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

@keyframes fades_in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.settings__blendsIn--animation {
  opacity: 0;
  animation: blendsIn 0.3s forwards cubic-bezier(0.77, 0, 0.18, 1);
  animation-delay: 0.1s;
  @for $i from 1 through 10 {
    &:nth-child(#{$i}) {
      animation-delay: $i * 0.02s;
    }
  }
}
@keyframes blendsIn {
  0% {
    transform: translateY(50px);
    opacity: 0;
  }
  100% {
    transform: translateY(0px);
    opacity: 1;
  }
}

.mainContainer__grid {
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: var(--spaceLrg);
  margin-top: var(--spaceMed);
  margin-bottom: var(--spaceMed);
}

.showTracklist__container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 300px;
  padding: var(--spaceMed);
  border-radius: var(--spaceSml);
  margin-bottom: var(--spaceMed);
  background: var(--dark);
  box-shadow: 5px 5px 16px 0 rgba(0, 0, 0, 0.15),
    -8px -8px 12px 0 rgba(0, 0, 0, 0.05);
}

.showTracklist__cta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: calc(300px - var(--spaceLrg));
  cursor: pointer;
}

.showTracklist__cta:hover > .showTracklist__title {
  color: var(--greenPrimary);
}

.showTracklist__cta:hover > .showTracklist__icon {
  fill: var(--greenPrimary);
}

.showTracklist__title {
  position: relative;
  font-weight: 700;
  margin-right: var(--spaceSml);
  transition: color 0.3s cubic-bezier(0.86, 0, 0.07, 1);
}

.showTracklist__title--glow {
  position: absolute;
  top: 0;
  left: 0;
  font-weight: 700;
  color: var(--greenPrimary);
  z-index: 0;
  opacity: 0;
  filter: blur(0px);
}

.showTracklist__title--glowIn {
  filter: blur(4px);
  opacity: 1;
  animation: glow_in 1s forwards;
}

@keyframes glow_in {
  0% {
    filter: blur(0px);
    opacity: 0;
  }
  100% {
    filter: blur(4px);
    opacity: 1;
  }
}

.showTracklist__title--glowOut {
  filter: blur(4px);
  opacity: 1;
  animation: glow_out 1s forwards;
}

@keyframes glow_out {
  0% {
    filter: blur(4px);
    opacity: 1;
    color: var(--greenPrimary);
  }
  100% {
    filter: blur(0px);
    opacity: 0;
    color: var(--light);
  }
}

.showTracklist__icon {
  fill: var(--light);
  height: var(--spaceSml);
  transform: rotate(90deg);
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: fill transform;
}

.showTracklist__title--isActive {
  color: var(--greenPrimary);
}

.showTracklist__icon--isActive {
  transform: rotate(-90deg);
  fill: var(--greenPrimary);
}

@media (max-width: 870px) {
  .mainContainer__grid {
    display: flex;
    flex-direction: column-reverse;
    width: 100%;
    gap: var(--spaceMed);
  }

  .showTracklist__container {
    width: 90vw;
  }

  .showTracklist__cta {
    width: 80vw;
  }
}
</style>
