<template>
  <div class="showTracklist__container">
    <div class="playlist__container">
      <div class="playlist__title">
        Playlist Name
      </div>
      <div class="playlis__mix--Synx">
        Synx Mix: <span class="playlis__mix--Artist">Chosen Artist</span>
      </div>
      <div class="playlist__cta">
        <div class="playlist__cta--title">Public</div>
        <input class="public__ctaBtn" type="checkbox" id="switchPublic" /><label
          for="switchPublic"
          >Toggle</label
        >
      </div>
      <div class="playlist__cta">
        <div class="playlist__cta--title">Collaborative</div>
        <input
          class="collaborative__ctaBtn"
          type="checkbox"
          id="switchCollaborative"
        /><label for="switchCollaborative">Toggle</label>
      </div>
      <button
        @click="btnActive"
        :class="{ 'buttonClicked--isActive': showBtnActive }"
      >
        <svg
          v-if="showBtnActive"
          xmlns="http://www.w3.org/2000/svg"
          width="8.4667mm"
          height="8.4667mm"
          viewBox="0 0 24 24"
          class="playlist__icon--success"
          :class="{ 'playlist__icon--isActive': showBtnActive }"
        >
          <path
            class="cls-1"
            d="M8.6782,20.1781a1.5,1.5,0,0,1-1.0605-.4395L.9395,13.0609a1.5,1.5,0,1,1,2.1211-2.1216L8.6768,16.555,20.9375,4.263a1.5,1.5,0,0,1,2.125,2.1182L9.74,19.7377a1.5018,1.5018,0,0,1-1.061.44Z"
          />
        </svg>
        <div
          class="playlist__buttonTitle"
          :class="{ 'playlist__buttonTitle--isActive': showBtnActive }"
        >
          {{ this.btnMessageDefault }}
        </div>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Playlist",
  data() {
    return {
      showBtnActive: false,
      btnMessageDefault: "Save Playlist to Spotify",
    };
  },
  methods: {
    btnActive: function() {
      this.showBtnActive = !this.showBtnActive;

      if (this.showBtnActive === true) {
        this.btnMessageDefault = "Playlist Saved";
      } else {
        this.btnMessageDefault = "Save Playlist to Spotify";
      }
    },
  },
};
</script>

<style scoped lang="scss">
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
}

.playlist__container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
  gap: var(--spaceSml);
  width: calc(300px - var(--spaceLrg));
}

.playlist__title {
  margin-bottom: var(--spaceSml);
  font-weight: 700;
}

.playlis__mix--Artist {
  font-weight: 700;
  color: var(--greenPrimary);

  margin-left: var(--spaceSml);
}

.playlist__cta {
  display: flex;
}

.playlist__cta--title {
  margin-right: var(--spaceSml);
}

/* CTA Section */
input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  cursor: pointer;
  text-indent: -9999px;
  width: 30px;
  height: 15px;
  background: var(--MedGrey);
  display: block;
  border-radius: 100px;
  position: relative;
}

label:after {
  content: "";
  position: absolute;
  top: 0px;
  left: 0px;
  width: 15px;
  height: 15px;
  background: var(--light);
  border-radius: 30px;
  transition: 0.3s;
}

input:checked + label {
  background: var(--greenPrimary);
}

input:checked + label:after {
  left: calc(100%);
  transform: translateX(-100%);
}

label:active:after {
  width: 15px;
}

button {
  width: 100%;
  border: none;
  font-size: var(--body-firstFont);
  font-weight: 700;
  color: var(--light);
  display: flex;
  justify-content: center;
  align-items: center;
  /*background: var(--greenPrimary);*/
  background: linear-gradient(45deg, #47917d 0%, #1c3c34 100%);
  background-size: 400px 50px;
  padding: var(--spaceSml);
  border-radius: var(--spaceLrg);
  cursor: pointer;
  margin-top: var(--spaceSml);
  box-shadow: 5px 5px 16px 0 rgba(0, 0, 0, 0.2),
    -8px -8px 12px 0 rgba(255, 255, 255, 0.08);
  transition: 0.5s cubic-bezier(0.86, 0, 0.07, 1);
}

button:hover {
  // background: var(--beige);
  background-size: 1000px 50px;
}

.buttonClicked--isActive {
  transform: translateX(15px);
  background-size: 1000px 50px;
  transition: all 1s cubic-bezier(0.86, 0, 0.07, 1);
  transition-property: transform background-size;
}

.buttonClicked--isActive:hover {
  // opacity: 0.75;
}

.playlist__icon--success {
  height: var(--spaceSml);
  width: auto;
  fill: var(--light);
  margin-right: var(--spaceSml);
  transform: translateX(30px);
  opacity: 0;
}

.playlist__buttonTitle {
  animation: slides_back 0.75s cubic-bezier(0.86, 0, 0.07, 1);
}

.playlist__buttonTitle--isActive {
  transform: translateX(0px);
  animation: slides_in_one 1s cubic-bezier(0.86, 0, 0.07, 1);
}

@keyframes slides_in_one {
  0% {
    opacity: 0;
    transform: translateX(-15px);
  }
  100% {
    opacity: 1;
    transform: translateX(0px);
  }
}

@keyframes slides_back {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.playlist__icon--isActive {
  opacity: 1;
  transform: translateX(0px);
  animation: slides_in_two 1.2s cubic-bezier(0.86, 0, 0.07, 1);
}

@keyframes slides_in_two {
  0% {
    opacity: 0;
    transform: translateX(30px);
  }
  25% {
    opacity: 0;
    transform: translateX(30px);
  }
  100% {
    opacity: 1;
    transform: translateX(0px);
  }
}

@media (max-width: 870px) {
  .showTracklist__container {
    width: 90vw;
  }

  .playlist__container {
    width: 80vw;
  }

  button {
    background-size: 150% 50px;
  }

  button:hover {
    background-size: 500% 50px;
  }

  .buttonClicked--isActive {
    background-size: 1000% 50px;
  }

  .buttonClicked--isActive:hover {
    background-size: 2000% 50px;
  }
}
</style>
