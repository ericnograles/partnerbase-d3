<template>
  <div class="container">
    <Nuxt/>
  </div>
</template>

<style>
html {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI",
    Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  color: #2E495E;
}

:root {
  --navy: #03313f;
  --cyan: #77d9e2;
  --red: #f53251;
  --grey7: #f8f8f8;
  --white: #ffffff;
  --grey6: #eaeaea;
  --grey5: #eaeaea;
  --grey3: #bebebe;
  --grey2: #b5b5b5;
  --grey1: #8b8b8b;
  --pink: #ed6d99;
  --purple: #ca6aca;
  --ice-blue: #ebfafb;
  --yellow: #fcb827;
  --dark-yellow: #df9b0a;
  --green: #7ecd6e;
  --orange: #f7821b;
  --black: #000000;
  --blue: #2682ae;
  --grey4: #d0d0d0;
  --grey5: #d8d8d8;
  --concrete-grey: #dcdedf;
  --ice-grey: #dbe2e4;
  --cyan-15: rgba(119, 217, 226, 0.15);
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #00C48D;
  color: #00C48D;
  text-decoration: none;
  padding: 10px 30px;
  display: inline-flex;
  align-self: center;
}

.button--green:hover {
  color: #fff;
  background-color: #00C48D;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #2E495E;
  color: #2E495E;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #2E495E;
}
</style>
