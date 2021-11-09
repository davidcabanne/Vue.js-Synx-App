<template>
  <router-view />
</template>

<style lang="scss">
:root {
  --white: #ffffff;
  --light: #efeff3;
  --lightGrey: #f2f2f2;
  --MedGrey: #bcbcbc;
  --ctaGrey: #757278;
  --black: #121213;
  --dark: #2e2e30;
  --darker: #1d1d1e;
  --darth: #4f3b51;
  --darkgrey: #3d3c3e;
  --red: #d1515a;
  --blue: #091f43;
  --greenPrimary: #47917d;
  --greenDark: #1c3c34;
  --beige: #bb8a52;
  --yellow: #ffba00;

  /* font-sizes: */
  --mainFont: "Inter";
  --headingFont: "Epilogue";
  --body-firstFont: 16px;
  --body-secondFont: 20px;
  --headingFirst: 25px;
  --headingSecond: 31.25px;
  --headingThird: 39.06px;
  --headingFourth: 48.83px;
  --largeFirst: 61.04px;
  --largeSecond: 76.29px;
  /* margin & padding */
  --spaceSml: 15px;
  --spaceMed: 30px;
  --spaceLrg: 60px;
  --maxWidth: 540px;
  /* icon size */
  --iconSize: 20px;
  /* post img */
  --imgMedium: 300px;
  --imgLarge: 400px;
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

*:focus {
  outline: none;
  opacity: 1;
}

a {
  text-decoration: none;
  color: var(--greenLight);
}

ul {
  list-style: none;
}

html {
  scroll-behavior: smooth;
}

body {
  font-size: var(--body-firstFont);
  color: var(--light);
  font-weight: 500;
  overflow-x: hidden;
  // background: linear-gradient(75deg, var(--dark), var(--darth));
  // background: linear-gradient(
  //   75deg,
  //   var(--darker),
  //   var(--darker),
  //   var(--greenDark)
  // );
  width: 100vw;
  min-height: 100vh;
}

#app {
  font-family: "Inter", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* FLEX STYLES */
.flex__regular {
  display: flex;
}
.flex__ctr {
  display: flex;
  justify-content: center;
  align-items: center;
}
.flex__col {
  flex-direction: column;
}

/* BLOC STYLES */
.bloc__container {
  width: 100vw;
}
.bloc__wrapper {
  width: 90vw;
  max-width: 1240px;
}
.bloc__marginSml {
  margin-top: var(--spaceSml);
}
.bloc__marginMed {
  margin-top: var(--spaceMed);
}
.bloc__marginLrg {
  margin-top: var(--spaceLrg);
}
</style>

<script>
//   <div id="nav">
//     <router-link to="/">Home</router-link> |
//     <router-link to="/about">About</router-link>
//   </div>
//   <router-view/>

//   #nav {
//   padding: 30px;
// }

// #nav a {
//   font-weight: bold;
//   color: #2c3e50;
// }

// #nav a.router-link-exact-active {
//   color: #42b983;
// }
</script>
