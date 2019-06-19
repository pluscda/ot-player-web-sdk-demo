<template>
  <div id="app">
      <!-- 1. The <iframe> (and video player) will replace this <div> tag. -->
    <div id="player_aotter1"></div>
  
    <!-- 2. The image loader. -->
    <a id="player_aotter2" data-trek="URL" data-bg-color="#ccc">
        <img data-trek="IMG_ICON_MAIN" />
        <h4 data-trek="TITLE"></h4>
        <h4 data-trek="TEXT"></h4>
    </a>

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
                config =  {
                        id: "player_aotter2",
                        loadType: 'BANNER',
                        events: {
                        cbAdLoaded: this.cbAdLoaded,
                        cbAdFailed: this.cbAdFailed,
                        cbAdImpression: this.cbAdImpression,
                        }
                };
                new AotterPlayer(config);
                clearInterval(checkLoaded);
            }
    }, 100);
    
  }
}
</script>

