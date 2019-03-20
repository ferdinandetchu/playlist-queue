<template>
  <div  style="margin-bottom: 41px;">
    <v-img :src="playing.src" height="200" cover v-if="playing">
      <v-layout fill-height style="background-color: rgba(250, 250, 250, 0.7)">
      </v-layout>
    </v-img>
    <v-container class="mycontainer mt-0">
      <div class="card" v-if="playing">
        <v-layout row wrap>
          <v-flex xs7 md3 xl2>
            <v-img class="elevation-5" :src="playing.src" height="175" width="175" style="border: 10px solid white;"/>
          </v-flex>
          <v-flex xs5 md6>
            <div class="black--text">
              <h5 style="filter: blur(0.2px);">{{playing.album}}</h5>
              <h1>{{playing.name}}</h1>
              <h3 style="color: #4f7675;">{{playing.title}}</h3>
            </div>
          </v-flex>
        </v-layout>
      </div>
      <div class="mysongs">
        <v-layout column wrap align center>
          <v-flex xs6>
            <v-layout row wrap>
              <v-flex xs2 md1>

              </v-flex>
              <v-flex xs4>
                <span>TItle</span>
              </v-flex>
              <v-flex xs2 md3 class="show">
                <span >play</span>
              </v-flex>
              <v-flex xs4>
                <span>menu</span>
              </v-flex>
            </v-layout>
          </v-flex>
          <v-flex xs6>
            <song-item v-for="(song, index) in songs" :song="song" :key="index" class="mymusic" />
          </v-flex>
        </v-layout>
      </div>
    </v-container>
    <footer class="myfooter" v-if="playing">
      <div class="text-xs-center">
        <div>
          <v-card tile dark style="background-color: rgba(17, 17, 17, 0.1);">
            <v-progress-linear
              :value="10"
              class="my-0 hidden-sm-and-up"
              height="3"
            ></v-progress-linear>
            <v-layout row wrap justify-center align-center style="padding-left: 15px; padding-right: 20px; background-color: rgba(17, 17, 17, 0.7);">
              <v-flex xs6 md2>
                <v-layout row wrap>
                  <v-flex xs3 py-2>
                    <v-layout justify-center align-center column fill-height>
                      <v-img :src="playing.src" height="50" class="elevation-11" style="width: 100%;" />
                    </v-layout>
                  </v-flex>
                  <v-flex xs9>
                    <v-layout justify-center align-start column fill-height>
                      <v-card-title primary-title>
                        <div style="width: 100%;" class="text-truncate text-xs-left">
                          <h2 class="text-truncate font-weight-medium" style="font-size: 14px;">{{playing.title}}</h2>
                          <h3 class="text-truncate font-weight-regular" style="font-size: 12px;">{{playing.name}}</h3>
                        </div>
                      </v-card-title>
                    </v-layout>
                  </v-flex>
                </v-layout>
              </v-flex>
              <v-flex xs6 md2>
                <v-layout justify-center align-center column fill-height>
                  <v-card-actions>
                    <v-btn icon @click="prevSong()">
                      <v-icon>fast_rewind</v-icon>
                    </v-btn>
                     <v-btn icon @click=" play = ! play">
                      <v-icon>{{ (!play) ? 'play_arrow' : 'pause' }}</v-icon>
                    </v-btn>
                    <v-btn icon @click="nextSong()">
                      <v-icon>fast_forward</v-icon>
                    </v-btn>
                    <v-btn icon  class="hidden-sm-and-up">
                      <v-icon>list</v-icon>
                    </v-btn>
                    <v-btn icon  class="hidden-sm-and-up">
                      <v-icon>volume_up</v-icon>
                    </v-btn>
                  </v-card-actions>
                </v-layout>
              </v-flex>
              <v-flex md4 class="hidden-sm-and-down">
                <v-layout row wrap>
                  <v-flex xs11>
                    <v-layout justify-center align-center column fill-height>
                      <v-progress-linear
                        :value="10"
                        class="my-0"
                        height="3"
                      ></v-progress-linear>
                    </v-layout>
                  </v-flex>
                  <v-flex xs1>
                    <v-layout justify-center align-center column fill-height>
                      <h4 style="font-size: 10px; color: #4f7675;" class="show white--text">-233</h4>
                    </v-layout>
                  </v-flex>
                </v-layout>
              </v-flex>
              <v-flex md4 class="hidden-sm-and-down">
                <v-layout row wrap>
                  <v-flex md6>
                    <v-layout justify-center align-center fill-height>
                      <v-btn icon>
                        <v-icon>list</v-icon>
                      </v-btn>
                      <v-btn round class="text-capitalize show" color="#6aa0f6">kymatb</v-btn>
                      <v-icon>volume_up</v-icon>
                    </v-layout>
                  </v-flex>
                  <v-flex md6 class="hidden-sm-and-down">
                    <v-layout justify-center align-center column fill-height>
                      <v-progress-linear
                        :value="10"
                        class="my-0"
                        height="3"
                      ></v-progress-linear>
                    </v-layout>
                  </v-flex>
                </v-layout>
              </v-flex>
            </v-layout>
            <!-- <v-list style="padding-left: 15px; padding-right: 20px; background-color: rgba(0, 0, 0, 0.5);">
              <v-list-tile>
                <v-img :src="playing.src" style="height: 50px; width: 50px; margin-right: 11px; border: solid;" />
                <v-list-tile-content>
                  <v-list-tile-title>{{playing.title}}</v-list-tile-title>
                  <v-list-tile-sub-title>{{playing.name}}</v-list-tile-sub-title>
                </v-list-tile-content>

                <v-list-tile-action>
                  <v-btn icon @click="prevSong()">
                    <v-icon>fast_rewind</v-icon>
                  </v-btn>
                </v-list-tile-action>

                <v-list-tile-action :class="{ 'mx-0': $vuetify.breakpoint.mdAndUp }">
                  <v-btn icon @click=" play = ! play">
                    <v-icon>{{ (!play) ? 'play_arrow' : 'pause' }}</v-icon>
                  </v-btn>
                </v-list-tile-action>

                <v-list-tile-action :class="{ 'mr-0': $vuetify.breakpoint.mdAndUp }">
                  <v-btn icon @click="nextSong()">
                    <v-icon>fast_forward</v-icon>
                  </v-btn>
                </v-list-tile-action>
                  <v-progress-linear
                    :value="10"
                    class="my-0"
                    height="3"
                  ></v-progress-linear>
                  <span style="font-size: 10px; color: #4f7675;" class="show">-233</span>
                  <v-btn icon>
                    <v-icon>list</v-icon>
                  </v-btn>
                  <v-btn round class="text-capitalize show" color="#6aa0f6">kymatb</v-btn>
                  <v-icon>volume_up</v-icon>
                  <v-progress-linear
                    :value="10"
                    class="my-0"
                    height="3"
                    style="width: 10%;"
                  ></v-progress-linear>
              </v-list-tile>
            </v-list> -->
          </v-card>
        </div>

      </div>
    </footer>
  </div>
</template>

<script>
import { EventBus } from '../Events.js'
import SongItem from '@/components/SongItem'
  export default {
    components: {
      SongItem
    },
    data () {
      return {
        play: true,
        value: 0,
        buffer: 10,
        bufferValue: 20,
        interval: 0,
        songs: [
          { title: 'Happiness', name:'Frank Edward', album: 'Ep Anb60M', src: '../images/head1.jpg' },
          { title: 'Ebiebi', name:'Jerry K Ft Victor & Nolly', album: 'Ep Anb60M', src: '../images/head2.jpg' },
          { title: 'Abba Father', name:'Daddy D Ft Prosper Menko', album: 'Ep Anb60M', src: '../images/E2.jpeg' },
          { title: 'Facts', name:'Lecrea', album: 'Lecrea', src: '../images/event1.jpg' },
          { title: 'Your Grace', name:'NF', album: 'Ep Anb60M', src: '../images/header1.png' },
          { title: 'Feel Good', name:'De Promiz', album: 'Ep Anb60M', src: '../images/header2.png' },
          { title: 'Translated', name:'The King', album: 'Ep Anb60M', src: '../images/me.jpeg' },
          { title: 'I Sing For You', name:'Mighty Ray', album: 'Ep Anb60M', src: '../images/head1.jpg' },
          { title: 'Boating', name:'NJ', album: 'Ep Anb60M', src: '../images/head1.jpg' },
          { title: 'Eternal Life', name:'Katalyst', album: 'Ep Anb60M', src: '../images/head1.jpg' }
        ],
        playing: null
      }
    },
    methods: {
      prevSong(index) {

        let songIndex = this.songs.findIndex(x => x.title == this.playing.title)

        let songLength = this.songs.length

        if (songIndex == 0) {

          EventBus.$emit('playNow', this.songs[(songLength - 1)]) 

        } else {

          EventBus.$emit('playNow', this.songs[(songIndex - 1)]) 

        }
      },
      nextSong(){

        let songIndex = this.songs.findIndex(x => x.title == this.playing.title) + 1

        if (this.songs.length == songIndex) {

          EventBus.$emit('playNow', this.songs[0]) 

        } else {

          EventBus.$emit('playNow', this.songs[songIndex]) 

        }
      }
    },

    mounted() {
      EventBus.$on('isPlaying', data => {
        this.playing = Object.assign({}, data)
      })
    }

  };
</script>
<style>

.myfooter{
  position: fixed;
  bottom: 0;
  width: 100%;
}
.mymusic:hover{
  box-shadow: 0px 2px 4px -1px rgba(0,0,0,0.2), 0px 4px 5px 0px rgba(0,0,0,0.14), 0px 1px 10px 0px rgba(0,0,0,0.12) !important;
}
/* medium, larg and extra-larg  */
@media only screen and (min-width: 993px){
  .card{
    position: relative;
    bottom: 79px;

  }
}
/* small and extra-small*/
@media only screen and (max-width: 993px){
  .show{
    display: none;
  }
  .prog_width{
    width: 80% !important;
  }
  .card{
    position: relative;
    bottom: 183px;

  }
  .mycontainer{
    margin-top: 68px !important;
  }
  .mysongs{
    margin-top: -108px;
  }
}
</style>
