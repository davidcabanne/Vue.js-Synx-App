<template>
  <div class="range-slider__container">
    <div class="range-slider__title">{{ this.settingsOpt.title }}</div>
    <div class="range-slider">
      <input type="range" min="0" max="100" step="1" v-model="sliderMin" />
      <input type="range" min="0" max="100" step="1" v-model="sliderMax" />
    </div>
    <div class="range-slider__footer">
      <div class="range-slider__value">{{ settingsOpt.minValue }}</div>
      <div class="range-slider__value">{{ settingsOpt.maxValue }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Settings",
  props: ["settingsOpt"],
  data() {
    return { minAngle: 0, maxAngle: 100 };
  },
  computed: {
    sliderMin: {
      get: function() {
        var val = parseInt(this.minAngle);
        return val;
      },
      set: function(val) {
        val = parseInt(val);
        if (val > this.maxAngle) {
          this.maxAngle = val;
        }
        this.minAngle = val;
      },
    },
    sliderMax: {
      get: function() {
        var val = parseInt(this.maxAngle);
        return val;
      },
      set: function(val) {
        val = parseInt(val);
        if (val < this.minAngle) {
          this.minAngle = val;
        }
        this.maxAngle = val;
      },
    },
  },
};
</script>

<style scoped lang="scss">
.range-slider__container,
.range-slider,
.range-slider__footer {
  width: calc(300px - var(--spaceLrg));
}

.range-slider__container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
  margin-top: var(--spaceMed);
  margin-bottom: var(--spaceMed);
}

.range-slider__container:first-child {
  margin-top: 40px;
}

.range-slider__container:last-child {
  margin-bottom: 0px;
}

.range-slider__title {
  margin-bottom: var(--spaceMed);
  font-weight: 700;
}

.range-slider {
  position: relative;
}

.range-slider input[type="range"] {
  position: absolute;
  left: 0;
  bottom: 0;
}

input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
}

input[type="range"]:focus {
  outline: none;
  opacity: 1;
}

input[type="range"]:focus::-webkit-slider-runnable-track {
  background: var(--MedGrey);
  opacity: 1;
}

input[type="range"]:focus::-ms-fill-lower {
  background: var(--MedGrey);
  opacity: 1;
}

input[type="range"]:focus::-ms-fill-upper {
  background: var(--MedGrey);
  opacity: 1;
}

input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 3px;
  cursor: pointer;
  background: var(--MedGrey);
  box-shadow: none;
  border: 0;
}

input[type="range"]::-webkit-slider-thumb {
  z-index: 2;
  position: relative;
  border: none;
  height: var(--spaceSml);
  width: var(--spaceSml);
  border-radius: var(--spaceSml);
  background: var(--light);
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -6px;
  box-shadow: 2px 2px 18px 0 rgba(239, 239, 243, 0.15),
    -2px -2px 18px 0 rgba(239, 239, 243, 0.05);
}

.range-slider__footer {
  display: flex;
  justify-content: space-between;
  margin-top: var(--spaceSml);
}

.range-slider__value {
  color: var(--greenPrimary);
}

@media (max-width: 870px) {
  .range-slider__container,
  .range-slider,
  .range-slider__footer {
    width: 80vw;
  }
}
</style>
