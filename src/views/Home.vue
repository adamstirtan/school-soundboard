<template>

  <v-app-bar :elevation="1" color="primary">

    <v-app-bar-nav-icon to="/" icon="mdi-speaker-wireless"></v-app-bar-nav-icon>
    <v-app-bar-title>GAA Gymnasium A/V</v-app-bar-title>
    <v-spacer></v-spacer>
    <v-btn
      v-if="playingSound"
      @click="$event => stopClicked()"
      class="me-2 text-none"
      prepend-icon="mdi-stop">
      Stop
    </v-btn>

  </v-app-bar>

  <v-container class="ma-4">

    <v-row>
      <h1>Songs</h1>
    </v-row>

    <v-row>

      <v-col class="pl-0"
        v-for="song in songs"
        :key="song.id"
        cols="12" sm="6" md="4" lg="3">

        <v-card :color="song.color">

          <v-card-title>{{ song.title }}</v-card-title>
          <v-card-subtitle>{{ song.subtitle }}</v-card-subtitle>

          <v-card-actions>
            <v-btn @click="$event => playClicked(song.id)">
              Play
            </v-btn>
          </v-card-actions>

        </v-card>

      </v-col>
      
    </v-row>

    <v-row>
      <h1>Sounds</h1>
    </v-row>

    <v-row>

  <v-col class="pl-0"
    v-for="sound in sounds"
    :key="sound.id"
    cols="12" sm="6" md="4" lg="3">

    <v-card :color="sound.color">

      <v-card-title>{{ sound.title }}</v-card-title>
      <v-card-subtitle>{{ sound.subtitle }}</v-card-subtitle>

      <v-card-actions>
        <v-btn @click="$event => playClicked(sound.id)">
          Play
        </v-btn>
      </v-card-actions>

    </v-card>

  </v-col>

  </v-row>

  </v-container>
  
</template>

<script setup>

import { ref, onMounted } from 'vue'

const songs = ref([
  { id: 1, title: 'Oh Canada', color: 'red', subtitle: 'English' },
  { id: 2, title: 'Oh Canada', color: 'red', subtitle: 'French' },
  { id: 3, title: 'Happy Birthday', color: 'blue', subtitle: 'Music only' },
  { id: 4, title: 'Happy Birthday', color: 'purple', subtitle: 'Music & lyrics' }
])

const sounds = ref([
  { id: 100, title: 'Attention', color: 'green', subtitle: 'Clap, clap, clap-clap-clap!' },
  { id: 101, title: 'Fart', color: 'brown', subtitle: 'Blame someone else!' },
  { id: 102, title: 'Drum roll', color: 'indigo', subtitle: 'And the winner is...' },
  { id: 103, title: 'Applause', color: 'green', subtitle: 'Congratulations, you are awesome' },
  { id: 104, title: 'Buzzer', color: 'red', subtitle: "Bzzzzzzzzt!" },
])

const playingSound = ref(null)
const audio = ref(new Audio())

const playClicked = function(id) {
  if (playingSound.value === id) {
    audio.value.pause()
    audio.value.currentTime = 0
    playingSound.value = null
  } else {
    audio.value.pause()
    audio.value.currentTime = 0
  }

  import(`@/assets/${id}.mp3`)
    .then((soundModule) => {
      audio.value.src = soundModule.default
      audio.value.play()
      playingSound.value = id
    })
}

const stopClicked = function() {
  audio.value.pause()
  audio.value.currentTime = 0
  playingSound.value = null
}

onMounted(() => {
  audio.value.addEventListener('ended', () => {
    playingSound.value = null
  })
})

</script>
