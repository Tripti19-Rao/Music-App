<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-tittle">
          {{ current.title }} - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title:"Rise and Fall",
          artist: "Adventure Club & Krewella",
          src: require("@/assets/Rise & Fall.mp3"),
        },
        {
          title: "Grateful",
          artist: "Neffex",
          src: require("@/assets/neffex-grateful.mp3"),
        },
        {
          title:"Arms around you",
          artist: "XXXTENTACION & Lil Pump",
          src: require("@/assets/Arms around you.mp3"),
        },
        {
          title:"Lemonade",
          artist: "Don Toliver, Gunna & NAV",
          src: require("@/assets/Lemonade.mp3"),
        },
        {
          title:"Pray",
          artist: "ILLENIUM",
          src: require("@/assets/Pray.mp3"),  
        },
        {
          title:"No Guidance",
          artist: "Ayzha Nyree",
          src: require("@/assets/No Guidance.mp3"),  
        },
        {
           title:"DJ Got Us Falling in Love",
          artist: "Usher",
          src: require("@/assets/DJ Got Us Falling in Love.mp3"),
        },
        {
          title:"Mine",
          artist: "Bazzi",
          src: require("@/assets/Mine.mp3"),
        },
        
        {
          title:"Bad Boy",
          artist: "Marwa Loud",
          src: require("@/assets/Bad Boy.mp3"),
        },
        {
          title: "Invinsible",
          artist: "Don Oliver",
          src: require("@/assets/deaf-kev-invincible.mp3"),
        },
        {
          title: "All I Ever Need",
          artist: "Austin Mahone",
          src: require("@/assets/Austin Mahone - All I Ever Need.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function() {
          this.index++;

          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
          this.current = this.songs[this.index];
          this.play(this.current);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}
header {
  display: flex;
  justify-content: center;
  align-content: center;
  padding: 15px;
  background-color: darkcyan;
  color: #ffffff;
}
main {
  width: 100%;
  max-width: 766px;
  margin: 0 auto;
  padding: 25px;
}

.song-tittle {
  color: darkslategray;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-tittle span {
  font-weight: 900;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button: {
  opacity: 0.8;
}

.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 30px;
  margin: 0px 15px;
  border-radius: 50px;
  color: aliceblue;
  background-color: darkcyan;
}

.next,
.prev {
  font-size: 18px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 48px;
  color: aliceblue;
  background-color: darkcyan;
}
.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: darkslategray;
  font-size: 30px;
  font-weight: 500;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  color: darkcyan;
}

.playlist .song:hover {
  color: rgb(135, 214, 188);
}

.playlist .song.playing {
  color: #ffffff;
    border-radius: 50px;
  background-image: linear-gradient(to right, darkcyan, rgb(79, 202, 161));
}
</style>
