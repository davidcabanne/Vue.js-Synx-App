<template>
  <div class="track__container">
    <div class="track__container--bg"></div>
    <div class="track__wrapper">
      <div class="track__coverWrapper">
        <div class="track__playerContainer">
          <button
            @click="playPauseTrack"
            class="track__playerBtn"
            :class="{
              'track__playerBtn--clicked': isActive(),
            }"
            type="button"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="track__playIcon"
              :class="{
                'track__playIcon--isActive': isPaused(),
              }"
              viewBox="0 0 100 100"
            >
              <path
                class="cls-1"
                d="M78.158,51.843,25.842,82.048a2.1275,2.1275,0,0,1-3.191-1.843V19.795a2.1278,2.1278,0,0,1,3.191-1.843L78.159,48.157A2.1283,2.1283,0,0,1,78.158,51.843Z"
              />
            </svg>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="track__pauseIcon"
              :class="{
                'track__pauseIcon--isActive': isPlaying(),
              }"
              viewBox="0 0 24 24"
            >
              <path
                class="cls-1"
                d="M10.65,19.11V4.89C10.65,3.54,10.08,3,8.64,3H5.01C3.57,3,3,3.54,3,4.89V19.11C3,20.46,3.57,21,5.01,21H8.64C10.08,21,10.65,20.46,10.65,19.11Z"
              />
              <path
                class="cls-1"
                d="M21.0016,19.11V4.89c0-1.35-.57-1.89-2.01-1.89h-3.63c-1.43,0-2.01.54-2.01,1.89V19.11c0,1.35.57,1.89,2.01,1.89h3.63C20.4316,21,21.0016,20.46,21.0016,19.11Z"
              />
            </svg>
          </button>
        </div>
        <img
          class="track__cover"
          :class="{
            'track__cover--clicked': isActive(),
          }"
          :src="track.cover"
        />
      </div>
      <div class="track__infoContainer">
        <div class="track__infos">
          <div class="track__title">{{ track.title }}</div>
          <div class="track__artist">{{ track.artist }}</div>
        </div>
        <div class="track__duration">{{ formatTime(track.duration) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import formatTime from "../lib/formatTime";

export default {
  name: "Track",
  props: ["track", "activeTrackId", "activeTrackState"],
  data() {
    return {};
  },
  methods: {
    isActive: function() {
      return this.track.id === this.activeTrackId;
    },
    isPlaying: function() {
      if (this.track.id === this.activeTrackId) {
        return this.activeTrackState === "PLAYING";
      }
      return false;
    },
    isPaused: function() {
      if (this.track.id === this.activeTrackId) {
        return this.activeTrackState === "PAUSED";
      }
      return true;
    },
    playPauseTrack: function() {
      this.$emit("play-pause-track", this.track.id);
    },
    formatTime: function(seconds) {
      return formatTime(seconds);
    },
  },
};
</script>

<style scoped lang="scss">
.track__container {
  position: relative;
  width: 100%;
  height: 100px;
  margin-top: var(--spaceMed);
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.track__container--bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--greenPrimary);
  opacity: 0.02;
  border-radius: 5px var(--spaceSml) var(--spaceSml) 5px;
  transition: 0.3s ease-in-out;
}

.track__container:hover > .track__container--bg {
  opacity: 0.3;
}

.track__wrapper {
  width: 100%;
  display: flex;
}

.track__coverWrapper {
  position: relative;
  height: 100px;
  width: 100px;
  display: flex;
  flex-shrink: 0;
  justify-content: center;
  align-items: center;
  margin-right: var(--spaceMed);
  border-radius: 5px;
  overflow: hidden;
}

.track__cover {
  position: absolute;
  top: 0;
  left: 0;
  width: auto;
  height: 100%;
  object-fit: cover;
  z-index: -1;
  transform: scale(1);
  transition: 0.2s ease-in-out;
}

.track__container:hover
  > .track__wrapper
  > .track__coverWrapper
  > .track__cover {
  transform: scale(1.05);
  transform-origin: center;
}

.track__cover--clicked {
  transform: scale(1.05);
  transform-origin: center;
}

.track__infoContainer {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  margin-bottom: var(--spaceSml);
}

.track__infos {
  max-width: 60%;
  z-index: 1;
}

.track__duration {
  margin-right: var(--spaceMed);
  z-index: 1;
}

.track__title,
.track__artist {
  cursor: pointer;
}

.track__title {
  font-weight: 700;
  margin-bottom: var(--spaceSml);
}

.track__artist {
  color: var(--greenPrimary);
}

.track__playerContainer {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.track__playerBtn {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  border-radius: 50px;
  background: var(--darker);
  border: none;
  cursor: pointer;
  opacity: 0;
  box-shadow: 5px 5px 16px 0 rgba(0, 0, 0, 0.75),
    -8px -8px 12px 0 rgba(255, 255, 255, 0.3);
  transform: scale(0);
  transition: 0.2s ease-in-out;
}

.track__playIcon,
.track__pauseIcon {
  position: absolute;
  fill: var(--light);
  width: 25px;
  height: auto;
  transform: translateX(1px);
  transition: 0.2s ease-in-out;
}

.track__pauseIcon {
  transform: translateX(0px);
}

.track__container:hover
  > .track__wrapper
  > .track__coverWrapper
  > .track__playerContainer
  > .track__playerBtn {
  opacity: 1;
  transform: scale(1);
}

.track__playerBtn--clicked {
  opacity: 1;
  transform: scale(1);
}

// .track__playIcon {
//   opacity: 1;
// }

// .track__pauseIcon {
//   opacity: 0;
// }

// .track__playIcon--isActive {
//   opacity: 0;
// }

// .track__pauseIcon--isActive {
//   opacity: 1;
// }

.track__playIcon {
  opacity: 0;
}

.track__pauseIcon {
  opacity: 0;
}

.track__playIcon--isActive {
  opacity: 1;
}

.track__pauseIcon--isActive {
  opacity: 1;
}

.track__playerBtn:hover > .track__playIcon,
.track__playerBtn:hover > .track__pauseIcon--isActive {
  fill: var(--greenPrimary);
}
</style>
