<template>
  <div id="app">
     <div id="player_aotter1"> </div>
  </div>
</template>

<script>
export default {
  name: 'app',

  methods: {
    cbAdLoaded() {
      
    },
    cbAdFailed() {

    },
    cbAdImpression(){

    }
  },

  mounted() {
    let config =  {
       width: 650,
       height: 390,
       id: 'player_aotter1',
       loadType: 'VIDEO',
       events: {
        cbAdLoaded: this.cbAdLoaded,
        cbAdFailed: this.cbAdFailed,
        cbAdImpression: this.cbAdImpression,
       }
    };
    let tag = document.createElement('script');
    tag.src = 'http://localhost:8080/aotterPlayer.js?date=' + +new Date();
    let firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
    let checkLoaded = setInterval(() => {
            if(AotterPlayer && AotterPlayer.loaded){
                new AotterPlayer(config);
                clearInterval(checkLoaded);
            }
    }, 100);
    
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
