<template>
<div id="app">
  <header>
    <h1>My Music</h1>
    <img src="show-photo.jpg" alt="">
  </header>
  <main>
     <section class="player">
      <h2 class="song-title">{{current.title}}-<span>{{current.artist}}</span></h2>
      <div class="control">
        <button class="prev" @click="prev"><i class="fa-solid fa-backward"></i></button>
        <button class="play" v-if="!isPlaying" @click="play"><i class="fa-solid fa-play"></i></button>
        <button class="pause" v-else @click="pause"><i class="fa-solid fa-pause"></i></button>
        <button class="next" @click="next"><i class="fa-solid fa-forward"></i></button>
      </div>
     </section>
     <section class="playlist">
       <h3>The Playlist</h3>
       <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src ==current.src) ? 'song playing' : 'song'">
       {{song.title}} - {{song.artist}}
       
       </button>
     </section>
  </main>
</div>
</template>

<script>


export default {
name:'app',
data() {
  return{
    current:{},
    index:0,
    isPlaying: false,
    songs:[
      {
        title:'Beau Young Prince',
        artist:'Let Go',
        src:require('./assets/Beau Young Prince -Let Go.mp3')
      },
      {
        title:'Губы',
        artist:'Andro',
        src:require('./assets/Andro - Губы.mp3')
      },
      {
        title:'Blinding Lights',
        artist:'The Weeknd',
        src:require('./assets/the-weeknd-blinding-lights.mp3')
      },
      {
        title:'Mood',
        artist:'24kGoldn',
        src:require('./assets/24kgoldn-mood-feat-iann-dior(mp3bit.cc).mp3')
      }
    ],
    player: new Audio()
  }
},
methods:{
  play(song) {
    if (typeof song.src != "undefined"){
      this.current = song;

      this.player.src = this.current.src;
    }

      this.player.play();
      this.player.addEventListener('ended', function(){
       this.index++;
           if(this.index > this.songs.length -1) {
      this.index = 0;
    }
    
    this.current = this.songs[this.index];
    this.play(this.current);
      }.bind(this));

      this.isPlaying = true;

  },
  pause() {
    this.player.pause();
    this.isPlaying = false;

  },
  next() {
    this.index++;
    if(this.index > this.songs.length -1) {
      this.index = 0;
    }
    
    this.current = this.songs[this.index];
    this.play(this.current);

  },
  prev() {
    this.index--;
    if(this.index < 0)   {
      this.index = this.songs.length -1;
    }
    
    this.current = this.songs[this.index];
    this.play(this.current);
  }

},
  created () {
   this.current = this.songs[this.index];
   this.player.src =  this.current.src;
  //  this.player.play();
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing:border-box;
}
body{
  font-family: sans-serif;
  background:black;
  
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  color: #702ecc;
  background-color: black;
}
main{
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title{
  color:#fff;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span{
  font-weight: 400;
  font-style: italic;
  color: #fff;
}
.control{
  display: flex;
  justify-content: center;
  padding: 30px 15px;
  align-items: center;

}

button{
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
.play, .pause{
  font-size: 20px;
  font-weight: 700;
  padding: 25px 30px;
  margin: 0px 15px;
  border-radius: 50px;
  color: #fff;
 background-image: linear-gradient(to right, #702ecc, #5858ff);
  
}


.next, .prev{
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background:none;
}

button:hover{
  opacity: 0.6;
}
.playlist{
  padding: 0px 30px;
}
.playlist h3{
  color: #fff;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;

}
.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  color: #50238f;
}
.playlist .song:hover{
  color:#7e7ea9;
  

}
.playlist .song.playing{
  color:#fff;
 background-image: linear-gradient(to right, #763ec5, #4a66f2);
 

}

</style>
