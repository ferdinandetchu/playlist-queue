<template>
  <v-layout row wrap align-center :class="(isPlaying) ? 'playing-now' : ''">
    <v-flex xs2 md1>
      <v-img :src="song.src" style="height: 40px; width: 40px;" />
    </v-flex>
    <v-flex xs2 md4>
      <h5 class="text-truncate">{{song.name}}-{{song.title}}</h5>
    </v-flex>
    <v-flex xs2 md3>
      <v-layout row wrap align-center>
        <v-flex xs8 md11>
          <v-progress-linear
            :value="10"
            class="my-0 show prog_width"
            height="3"
            style="width: 194px;"
            round
          ></v-progress-linear>
        </v-flex>
        <v-flex xs4 md1>
          <span style="font-size: 10px; color: #4f7675;">-233</span>
        </v-flex>
      </v-layout>
    </v-flex>
    <v-flex xs6 md4>
      <v-layout row wrap align-center>
          <v-btn @click.stop="togglePlay(song)" color="#e51927" dark icon small>
            <v-icon >{{ (!isPlaying) ? 'play_arrow' : 'pause' }}</v-icon>
          </v-btn>
          <v-btn icon class="text-capitalize" @click.stop="isPlaying = ! isPlaying">
            <v-icon>share</v-icon>
            <span class="show">Share</span>
          </v-btn>
          <v-btn icon>
            <v-icon>save_alt</v-icon>
          </v-btn>
      </v-layout>
    </v-flex>
  </v-layout>
</template>

<script>
import { EventBus } from '../Events.js'
  export default {
    props: ['song'],

    data() {
      return {
        isPlaying: false,
      }
    },

    methods: {
      togglePlay(song) {
        EventBus.$emit('playNow', song)  
         }

    },

    mounted() {
      EventBus.$on('playNow', data => {
        if(data.title == this.song.title) {
          this.isPlaying = true;
          EventBus.$emit('isPlaying', this.song)
        } else {
          this.isPlaying = false
        }
      })
    }
  };
</script>

<style lang="css" scoped>
.playing-now {
  box-shadow: 0px 2px 4px -1px rgba(0,0,0,0.2), 0px 4px 5px 0px rgba(0,0,0,0.14), 0px 1px 10px 0px rgba(0,0,0,0.12) !important;
  background-color: #b8c1c1;
}
/* small and extra-small*/
@media only screen and (max-width: 993px){
  .show{
    display: none;
  }
}

</style>
