<template>
  <div id="app" class="wrapper">
    <router-view />
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  background: whitesmoke;
}

.wrapper {
  width: 90%;
  margin: 0 auto;
}

/* General */
p { margin: 0; }
h1 { font-weight: 400; }

@media (min-width: 992px) {
  .wrapper {
    width: 80%;
    margin: 0 auto;
  }
}

@media (min-width: 1800px) {
  .wrapper {
    width: 1525px;
    margin: 0 auto;
  }
}
</style>
