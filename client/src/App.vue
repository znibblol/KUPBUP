<template>
  <div id="app">
    <div class="nav">
      <h3>KUPBUP</h3> <h3><router-link to="/">Boards ></router-link></h3>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
  body {
    background: #0a2238;
  }

  .container {
    width: 100%;
    padding: 15px;
  }

  .nav {
    color: #FFF;
    width: 100%;
    height: 50px;
    background: rgba(0,0,0,0.2);
    // border-bottom: 1px solid rgba(255,255,255,0.2);
    box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
    display: flex;
    align-items: center;

    h3 {
      padding: 15px;
      font-weight: 300;
      
      a {
        color: #FFF;
        text-decoration: none;
        transition: all 500ms;
        padding: 15px;
        &:hover {
          background: rgba(255,255,255,0.1);
        }
      }
    }
  }
}

// Media queries
@media screen and (min-width: 800px) {
  .container {
    width: 80%;
    margin: auto;
  }
}
</style>
