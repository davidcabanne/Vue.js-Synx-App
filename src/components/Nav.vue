<template>
  <header class="bloc__container flex__ctr">
    <nav class="bloc__wrapper flex__ctr">
      <div class="nav__logo">
        <a href="#"><img class="nav__logo" src="../assets/logo-synx.svg"/></a>
      </div>
      <ul class="nav__links flex__ctr">
        <div @click="toggleBurger" class="burger__container">
          <span
            class="burger__line line__one"
            :class="{ 'line__one--isActive': toggleBurgerActive }"
          ></span>
          <span
            class="burger__line line__two"
            :class="{ 'line__two--isActive': toggleBurgerActive }"
          ></span>
          <span
            class="burger__line line__three"
            :class="{ 'line__three--isActive': toggleBurgerActive }"
          ></span>
        </div>
        <li class="nav__links--icon">Tracks</li>
        <li class="nav__links--icon">Artists</li>
        <li class="nav__links--icon">How it works</li>
        <li>
          <Dropdown />
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
import Dropdown from "./Dropdown";

export default {
  name: "Nav",
  components: {
    Dropdown,
  },
  data() {
    return {
      toggleBurgerActive: false,
    };
  },
  methods: {
    toggleBurger() {
      console.log("toggle burger");
      this.toggleBurgerActive = !this.toggleBurgerActive;
    },
  },
};
</script>

<style scoped>
nav {
  height: 80px;
  justify-content: space-between;
  align-items: flex-end;
}

.nav__logo {
  height: 30px;
  width: auto;
  cursor: pointer;
  transition: opacity 0.3s cubic-bezier(0.77, 0, 0.18, 1);
}
.nav__logo:hover {
  opacity: 0.75;
}

li {
  margin-right: var(--spaceMed);
  cursor: pointer;
}

li:last-child {
  margin-right: 0;
}

.nav__links--icon {
  transition: 0.3s ease-in-out;
}

.nav__links--icon:hover {
  color: var(--greenPrimary);
}

@media (max-width: 870px) {
  .nav__links--icon {
    display: none;
  }

  .burger__container {
    width: 30px;
    height: 20px;
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    flex-direction: column;
    margin-right: var(--spaceMed);
    cursor: pointer;
  }

  .burger__line {
    position: relative;
    width: 100%;
    height: 2px;
    background: var(--light);
    border-radius: 2px;
    opacity: 0.9;
    transition: all 0.3s cubic-bezier(0.86, 0, 0.07, 1);
    transition-property: background transform opacity width;
  }

  .burger__container:hover > .burger__line {
    background: var(--greenPrimary);
  }

  .line__one {
    width: 50%;
  }

  .line__one--isActive:after,
  .line__two--isActive:after,
  .line__three--isActive:after {
    position: absolute;
    content: "";
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: var(--light);
    filter: blur(5px);
  }

  .line__one--isActive {
    width: 100%;
    transform: translateY(8px) rotate(45deg);
  }
  .line__two--isActive {
    opacity: 0;
  }
  .line__three--isActive {
    transform: translateY(-10px) rotate(-45deg);
  }
}
</style>
