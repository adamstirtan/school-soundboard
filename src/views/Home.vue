<template>
  <v-app-bar :elevation="1" color="primary">
    <v-app-bar-nav-icon to="/" icon="mdi-play-circle"></v-app-bar-nav-icon>
    <v-app-bar-title>GAA Soundboard</v-app-bar-title>
    <v-spacer></v-spacer>
    <v-btn
      v-if="playingSound"
      @click="($event) => stopClicked()"
      class="me-2"
      prepend-icon="mdi-stop"
    >
      Stop
    </v-btn>
  </v-app-bar>

  <v-container fluid class="mx-2">
    <v-row>
      <h1>🎵 Songs</h1>
    </v-row>

    <v-row>
      <v-col
        class="pl-0"
        v-for="song in songs"
        :key="song.id"
        cols="12"
        md="3"
        sm="4"
      >
        <v-card :color="song.color">
          <v-card-title>{{ song.title }}</v-card-title>
          <v-card-subtitle>{{ song.subtitle }}</v-card-subtitle>

          <v-card-actions>
            <v-btn @click="($event) => playClicked(song.id)"> Play </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

    <v-row>
      <h1>📢 Sounds</h1>
    </v-row>

    <v-row>
      <v-col
        class="pl-0"
        v-for="sound in sounds"
        :key="sound.id"
        cols="12"
        md="2"
        sm="4"
      >
        <v-card :color="sound.color">
          <v-card-title>{{ sound.title }}</v-card-title>
          <v-card-subtitle>{{ sound.subtitle }}</v-card-subtitle>

          <v-card-actions>
            <v-btn @click="($event) => playClicked(sound.id)"> Play </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>

    <v-row justify="center">
      <p class="my-5">
        <small>
          <v-icon icon="mdi-github" />
          <a
            href="https://github.com/adamstirtan/gaa-gymnasium-av"
            target="_blank"
            >https://github.com/adamstirtan/gaa-gymnasium-av</a
          >
        </small>
      </p>
    </v-row>
  </v-container>
</template>
