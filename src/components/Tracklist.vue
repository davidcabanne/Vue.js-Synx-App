<template>
  <div class="tracklist__mainWrapper">
    <div class="tracklist__header">
      <div class="tracklist__mainTitle">
        Tracklist
      </div>
      <div class="tracklist__mainInfos">
        <div class="tracklist__mainInfos--nbr">{{ tracks.length }} tracks</div>
        <div class="tracklist__mainInfos--duration">
          {{ formatTime(totalDuration) }}
        </div>
      </div>
    </div>
    <div class="tracklist__tracksContainer">
      <Track
        v-for="track in tracks"
        :key="track.id"
        :track="track"
        :activeTrackId="tracks[activeTrackIndex].id"
        :activeTrackState="activeTrackState"
        @play-pause-track="playPauseTrack"
        class="loading__animation"
      />
    </div>
  </div>
  <!-- player Sect -->
  <div
    class="player__spacer"
    :class="{ 'showPlayer--isActive': showPlayerActive }"
  >
    <div
      class="player__container"
      :class="{ 'player__container--isActive': showPlayerActive }"
    >
      <div class="player__wrapper">
        <div class="track__wrapper">
          <div
            class="track__coverWrapper"
            :class="{ 'track__coverWrapper--isActive': showPlayerActive }"
          >
            <img
              class="track__cover"
              :class="{
                'track__cover--clicked': togglePlayActive,
              }"
              :src="tracks[activeTrackIndex].cover"
            />
          </div>
          <div
            class="track__infoContainer"
            :class="{ 'track__infoContainer--isActive': showPlayerActive }"
          >
            <div
              class="track__infos"
              :class="{ 'track__infos--isActive': showPlayerActive }"
            >
              <div
                class="track__title"
                :class="{ 'track__title--isActive': showPlayerActive }"
              >
                {{ tracks[activeTrackIndex].title }}
              </div>
              <div class="track__artist">
                {{ tracks[activeTrackIndex].artist }}
              </div>
            </div>
            <!-- right modules -->
            <div class="track__infos--right">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="3.0395mm"
                height="6.1238mm"
                viewBox="0 0 8.6159 17.3587"
                class="showTracklist__icon"
                @click="showPlayer"
                :class="{
                  'showPlayer__icon--isActive': showPlayerActive,
                }"
              >
                <path
                  d="M.7687,0a.7467.7467,0,0,1,.53.22l6.52,6.52a2.7349,2.7349,0,0,1,0,3.86l-6.52,6.52A.75.75,0,0,1,.2013,16.0974q.018-.0194.0374-.0374l6.52-6.52a1.2354,1.2354,0,0,0,0-1.7393L.2387,1.28A.75.75,0,0,1,.7687,0Z"
                />
              </svg>
              <div class="track__duration">
                {{ formatTime(tracks[activeTrackIndex].duration) }}
              </div>
            </div>
            <!-- right modules -->
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- player Sect -->
</template>

<script>
import Track from "@/components/Track";
import formatTime from "../lib/formatTime";

export default {
  name: "Tracklist",
  components: {
    Track,
  },
  data() {
    const tracks = [
      {
        id: 1,
        title: "Memory Residue",
        artist: "Anenon",
        cover:
          "https://geo-media.beatport.com/image_size/500x500/880047f6-f5b5-447f-afa9-979f21b3c4da.jpg",
        duration: 288,
      },
      {
        id: 2,
        title: "The Distance",
        artist: "Gaussian Curve",
        cover:
          "https://img.discogs.com/j-GufqMU4Ebw9qU6_Ota4fuKkI0=/fit-in/600x600/filters:strip_icc():format(jpeg):mode_rgb():quality(90)/discogs-images/R-9914274-1488460541-1085.jpeg.jpg",
        duration: 371,
      },
      {
        id: 3,
        title: "Reverse Culture Music",
        artist: "Steve Hauschildt",
        cover:
          "https://is2-ssl.mzstatic.com/image/thumb/Music113/v4/31/d9/f2/31d9f2e3-2591-acec-1681-3d79f1a64b53/804297834603.jpg/400x400bb.jpg",
        duration: 369,
      },
      {
        id: 4,
        title: "Forest Run",
        artist: "Joseph Shabason",
        cover:
          "https://i1.sndcdn.com/artworks-000392380905-53pg6y-t500x500.jpg",
        duration: 269,
      },
      {
        id: 5,
        title: "Reverie for Fragile Houseplants",
        artist: "Tomaga",
        cover: "https://f4.bcbits.com/img/a1432376908_10.jpg",
        duration: 270,
      },
      {
        id: 6,
        title: "Long Long Silk Bridge",
        artist: "Susumu Yokota",
        cover: "https://f4.bcbits.com/img/a1699237270_5.jpg",
        duration: 182,
      },
      {
        ìd: 7,
        title: "Ecce! Ego!",
        artist: "Leon Vynehall",
        cover:
          "https://direct.rhapsody.com/imageserver/images/alb.559464649/600x600.jpg",
        duration: 213,
      },
      {
        id: 8,
        title: "Exit Seven",
        artist: "Jonny Nash",
        cover:
          "https://i1.sndcdn.com/artworks-000109536130-33rhcz-t500x500.jpg",
        duration: 216,
      },
      {
        id: 9,
        title: "The Piano Drop",
        artist: "Tim Hecker",
        cover:
          "https://lastfm.freetls.fastly.net/i/u/ar0/9de43f0a02c8b0a3fe8996b3c75ad2fb.jpg",
        duration: 174,
      },
      {
        id: 10,
        title: "Why Like This?",
        artist: "Teebs",
        cover:
          "https://img.discogs.com/uV4n_9uSBltauQ5WM2CsZLbBSTc=/fit-in/600x596/filters:strip_icc():format(webp):mode_rgb():quality(90)/discogs-images/R-2597743-1538480398-9796.jpeg.jpg",
        duration: 177,
      },
    ];

    let totalDuration = 0;
    for (let i = 0; i < tracks.length; i++) {
      totalDuration += tracks[i].duration;
    }

    return {
      tracks: tracks,
      totalDuration: totalDuration,
      activeTrackIndex: 0,
      activeTrackState: "PAUSED",
      showPlayerActive: true,
    };
  },
  methods: {
    formatTime: function(seconds) {
      return formatTime(seconds);
    },
    showPlayer: function() {
      console.log("Show player");
      this.showPlayerActive = !this.showPlayerActive;
    },
    playPauseTrack: function(trackId) {
      const sameTrack = trackId === this.tracks[this.activeTrackIndex].id;
      if ((sameTrack && this.activeTrackState === "PAUSED") || !sameTrack) {
        console.log("playing track", trackId);
        this.activeTrackState = "PLAYING";
        // Play on player
      } else {
        console.log("pausing track", trackId);
        this.activeTrackState = "PAUSED";
        // Pause player
      }

      let trackIndex = null;
      for (let i = 0; i < this.tracks.length; i++) {
        if (this.tracks[i].id === trackId) {
          trackIndex = i;
        }
      }

      this.activeTrackIndex = trackIndex;
    },
  },
  mounted() {
    this.playPauseTrack(1);
  },
};
</script>

<style scoped lang="scss">
.loading__animation {
  opacity: 0;
  animation: blendIn 1s forwards cubic-bezier(0.77, 0, 0.18, 1);
  animation-delay: 0.5s;
  @for $i from 1 through 10 {
    &:nth-child(#{$i}) {
      animation-delay: $i * 0.1s;
    }
  }
}
@keyframes blendIn {
  0% {
    transform: translateY(30px);
    opacity: 0;
  }
  100% {
    transform: translateY(0px);
    opacity: 1;
  }
}

.tracklist__mainWrapper {
  display: flex;
  flex-direction: column;
}

.tracklist__header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}
.tracklist__mainTitle {
  font-size: var(--headingFirst);
  font-weight: 700;
}

.tracklist__mainInfos {
  display: flex;
}

.tracklist__mainInfos--nbr {
  margin-right: var(--spaceSml);
}

.player__spacer,
.player__container,
.player__container:after,
.player__wrapper {
  height: 100px;
}

.player__spacer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  transition: transform 0.3s ease-in-out;
}

.showPlayer--isActive {
  transform: translateY(50px);
  transition: 0.3s ease-in-out;
  transition-property: transform;
}

.player__container {
  position: relative;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}

.player__container:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  background: var(--darker);
  border-top: 1px solid var(--dark);
  box-shadow: 5px 5px 16px 0 rgba(0, 0, 0, 0.15),
    -8px -8px 12px 0 rgba(0, 0, 0, 0.05);
  border-radius: 8px 8px 0px 0px;
  transition: opacity 0.3s cubic-bezier(0.86, 0, 0.07, 1);
}

.player__container--isActive {
  opacity: 0.95;
}

.player__wrapper {
  width: 90vw;
  max-width: 1240px;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.track__wrapper {
  width: 100%;
  display: flex;
}

.track__coverWrapper {
  position: relative;
  height: 60px;
  width: 60px;
  display: flex;
  flex-shrink: 0;
  justify-content: center;
  align-items: center;
  margin-right: var(--spaceMed);
  border-radius: 5px;
  overflow: hidden;
  z-index: 1;
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: height width;
}

.track__coverWrapper--isActive {
  height: 20px;
  width: 20px;
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

.track__infoContainer {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}

.track__infoContainer--isActive {
  display: flex;
  align-items: flex-start;
}

.track__infos {
  display: flex;
  justify-content: flex-end;
  align-items: flex-start;
  flex-direction: column;
  max-width: 60%;
  height: 60px;
  z-index: 1;
  animation: opacity__out 0.5s cubic-bezier(0.86, 0, 0.07, 1);
}

.track__infos--isActive {
  flex-direction: row;
  animation: opacity__in 0.5s cubic-bezier(0.86, 0, 0.07, 1);
}

@keyframes opacity__in {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes opacity__out {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.track__infos--right {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
  max-width: 60%;
  height: 60px;
  z-index: 1;
}

.showTracklist__icon {
  fill: var(--light);
  height: var(--spaceSml);
  transform: rotate(90deg);
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: fill transform;
  cursor: pointer;
}

.showTracklist__icon:hover {
  fill: var(--greenPrimary);
}

.showPlayer__icon--isActive {
  transform: rotate(-90deg);
  fill: var(--greenPrimary);
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: transform fill;
}

.track__title,
.track__artist {
  cursor: pointer;
}

.track__title {
  font-weight: 700;
}

.track__artist {
  color: var(--greenPrimary);
}

.track__title--isActive {
  margin-right: var(--spaceSml);
  transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: margin;
}
</style>
