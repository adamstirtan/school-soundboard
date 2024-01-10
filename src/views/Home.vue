<template>
  <v-app-bar :elevation="1" color="primary">

    <v-app-bar-nav-icon to="/" icon="mdi-play-circle"></v-app-bar-nav-icon>
    <v-app-bar-title>GAA Soundboard</v-app-bar-title>
    <v-spacer></v-spacer>
    <v-btn v-if="playingSound" @click="$event => stopClicked()" class="me-2" prepend-icon="mdi-stop">
      Stop
    </v-btn>

  </v-app-bar>

  <v-container fluid class="mx-2">

    <v-row>
      <h1>🎵 Songs</h1>
    </v-row>

    <v-row>

      <v-col class="pl-0" v-for="song in songs" :key="song.id" cols="12" md="3" sm="4">

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
      <h1>👑 Principal for a day</h1>
    </v-row>

    <v-row>

      <v-col class="pl-0" v-for="song in principalsongs" :key="song.id" cols="12" md="3" sm="4">

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
      <h1>📢 Sounds</h1>
    </v-row>

    <v-row>

      <v-col class="pl-0" v-for="sound in sounds" :key="sound.id" cols="12" md="2" sm="4">

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

    <v-row justify="center">
      <p class="my-5">
        <small>
          <v-icon icon="mdi-github" /> <a href="https://github.com/adamstirtan/gaa-gymnasium-av" target="_blank">https://github.com/adamstirtan/gaa-gymnasium-av</a>
        </small>
      </p>
    </v-row>

  </v-container>
</template>

<script setup>

import { ref, onMounted } from 'vue'

const songs = ref([
  { id: 1, title: '🇨🇦 O Canada', color: 'red', subtitle: 'Classic, like maple syrup and hockey!' },
  { id: 2, title: '🎤 O Canada (Acapella)', color: 'red', subtitle: 'Do-do-dooooo' },
  { id: 3, title: '🥳 Happy Birthday', color: 'blue', subtitle: 'Sing-a-long' },
  { id: 4, title: '🎄 We wish you a Merry Christmas', color: 'grey', subtitle: '...and a happy new year' },
  { id: 5, title: '🤘 School\'s Out by Alice Cooper', color: 'purple', subtitle: 'No more pencils, no more books!' },
  { id: 6, title: '🍺 Chug jug with you', color: 'green', subtitle: 'Just wiped out tomato town' },
])

const principalsongs = ref([
  { id: 201, title: '👦🏼 Jack Stirtan', color: 'blue', subtitle: 'Principal of the day' },
  { id: 200, title: '👧🏼 Olivia Stirtan', color: 'blue', subtitle: 'Vice principal of the day' }
])

const sounds = ref([
  { id: 114, title: '🤣 Badum-ching!', color: 'teal', subtitle: "Nice one bruh" },
  { id: 100, title: '😵 Roblox ooof!', color: 'grey', subtitle: "I'm dead" },
  { id: 121, title: '🚨 Alert', color: 'yellow', subtitle: "Ahhhhh" },
  { id: 101, title: '💨 Fart', color: 'brown', subtitle: 'Blame someone else!' },
  { id: 102, title: '🥁 Drum roll', color: 'indigo', subtitle: 'And the winner is...' },
  { id: 120, title: '👑 Rizz', color: 'blue', subtitle: "Did you seeeee that?" },
  { id: 103, title: '👏 Applause', color: 'green', subtitle: 'Congratulations, you are awesome' },
  { id: 111, title: '☠️ Game over', color: 'black', subtitle: "And you're out of continues" },
  { id: 104, title: '🚨 Buzzer', color: 'red', subtitle: "Bzzzzzzzzt!" },
  { id: 105, title: '👎 Boooo', color: 'black', subtitle: "No one likes that" },
  { id: 112, title: '🚩 Stage complete!', color: 'blue', subtitle: "But the princess is in another castle :(" },
  { id: 106, title: '😯 Dun-dun-dun!', color: 'orange', subtitle: "Add some dramatic flair" },
  { id: 107, title: '🐄 Mooooo', color: 'white', subtitle: "What does the cow say?" },
  { id: 108, title: '📯 Fanfare', color: 'pink', subtitle: "Celebrate the little things" },
  { id: 109, title: '❌ Trombone slide', color: 'yellow', subtitle: "There's always next time" },
  { id: 110, title: '⏰ Alarm', color: 'red', subtitle: "Time to wake up!" },
  { id: 113, title: '🤦‍♂️ Bruh', color: 'purple', subtitle: "One word is all you need" },
  { id: 115, title: '🎉 Airhorn', color: 'amber', subtitle: "Make them look" },
  { id: 116, title: '💰 Cash register', color: 'green', subtitle: "Dollar bills ya'll" },
  { id: 117, title: '🚽 Skibidi toilet', color: 'brown', subtitle: "dop dop dop yes yes" },
  { id: 118, title: '🏆 0.0001% winrate', color: 'purple', subtitle: "Show em' who u r" },
  { id: 119, title: '💥 Emotional damage', color: 'orange', subtitle: "Hurts so bad" },
])

const playingSound = ref(null)
const audio = ref(new Audio())

const playClicked = function (id) {
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
  
  gtag('event', 'play', {
    'event_category': 'interaction',
    'event_label': 'play'
  })
}

const stopClicked = function () {
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

<style scoped>
h1 {
  margin-top: 1rem;
}
</style>