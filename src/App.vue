<template>
  <div id="app">
    <header>
      <h1>Raffia Music App</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} -
          <span>{{ current.artist }}</span>
        </h2>
        <div class="control">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play"><i class="fas fa-play icon"></i></button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>PlayList</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="(song.src == current.src) ? 'song playing' : 'song' "
        >{{ song.title }} - {{ song.artist }} - {{ song.year }}</button>
      </section>
    </main>
    <footer>
      App Built by <a href="mfonidomark.netlify.com"></a>
    </footer>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "No Love",
          artist: "August Alsina Ft Nicki_Minaj",
          year: 2018,
          src: require("./assets/August_Alsina_Ft_Nicki_Minaj_No_Love_Remix.mp3"),
        },
        {
          title: "Anybody",
          artist: "Burna Boy",
          year: 2019,
          src: require("./assets/Burna-Boy-Anybody.mp3"),
        },
        {
          title: "Because you love me",
          artist: "Celine Dion",
          year: 2013,
          src: require("./assets/Celine Dion- Becos U Love ME.mp3"),
        },
        {
          title: "Brass Band Praise",
          artist: "Ikot ekpene Brass band",
          year: 2015,
          src: require("./assets/brass praises mix-1.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {

    // this functions plays songs 

    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.player.addEventListener("ended", function () {
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },

    // this is the function to puase songs

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    // this is the function to play next song

    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },

    // this is the function to go back to previous song

    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },

  // this function actually makes the song to play

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background-image: url('https://images.unsplash.com/photo-1505740420928-5e560c06d30e?ixlib=rb-1.2.1&w=1000&q=80');
  background-size: cover;
  height: 100%;
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #fff;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  align-items: center;
  text-align: center;
  justify-content: center;
  padding: 25px;
}
.song-title {
  color: gray;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
  /* padding: 30px 15px; */
}
.control {
  display: flex;
  justify-content: space-evenly;
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
button:hover {
  opacity: 0.8;
}
.play {
  font-weight: 20px;
  font-weight: 700px;
  padding: 15px 25px;
  border-radius: 8px;
  color: #fff;
  background-color: rgb(1, 255, 86);
}
.pause {
  font-weight: 20px;
  font-weight: 700px;
  padding: 15px 25px;
  border-radius: 8px;
  color: #fff;
  background-color: rgba(255, 0, 0, 0.884);
}
.next, .prev {
  font-weight: 16px;
  font-weight: 700px;
  padding: 10px 20px;
  border-radius: 6px;
  color: #fff;
  background-color: rgba(134, 35, 35, 0.733);
}
.playlist{
   padding: 0px 30px;
}
.playlist > h3 {
  color: black;
  font-size: 45px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  color: #FF5858;
}
.playlist .song.playing{
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
.icon {
  font-size: 40px;
}
</style>
