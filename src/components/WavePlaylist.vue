<template>
    <div class="butonGroup">
      <div id="top-bar" class="playlist-top-bar">
        <div class="playlist-toolbar">
          <div class="btn-group">
            <span class="btn-pause btn btn-warning" v-on:click="pause"><i class="fa fa-pause">Pause</i></span>
            <span class="btn-play btn btn-success" v-on:click="start"><i class="fa fa-play">Start</i></span>
            <span class="btn-stop btn btn-danger" v-on:click="stop"><i class="fa fa-stop">Stop</i></span>
          </div>
        </div>
      </div>
      <div id="playlist"></div>
    </div>
</template>
<script>
  import '../styles/playlist.scss'
  var ee = null
  export default {
    name: 'wave-playlist',
    mounted: function () {
      var WaveformPlaylist = require('waveform-playlist')
      var playlist = WaveformPlaylist.init(
        {
          samplesPerPixel: 899,
          // ac: new (window.AudioContext || window.webkitAudioContext),
          // // sample rate of the project. (used for correct peaks rendering)
          // sampleRate: new (window.AudioContext || window.webkitAudioContext).sampleRate,
          mono: true,
          timescale: true,
          waveHeight: 200,
          container: document.getElementById('playlist'),
          state: 'cursor',
          colors: {
            waveOutlineColor: '#E0EFF1',
            timeColor: 'grey',
            fadeColor: 'black'
          },
          controls: {
            show: true,
            width: 200
          },
          zoomLevels: [512, 899, 1024, 2048, 4096],
          seekStyle: 'fill',
          isAutomaticScroll: true,
          isContinuousPlay: true
        }
        // EventEmitter()
      )

      ee = playlist.getEventEmitter()
      ee.on('finished', function () {
        console.log('The cursor has reached the end of the selection !')
      })

      playlist
        .load([
          {
            src: 'media/audio/track1.mp3',
            name: 'Vocals',
            // cuein: 2,
            selected: {
              start: 2
            },
            start: 2
            // fadeIn: {
            //   shape: "logarithmic",
            //   duration: 0.75
            // },
            // fadeOut: {
            //   shape: "logarithmic",
            //   duration: 1.5
            // }
          },
          {
            src: 'media/audio/track2.mp3',
            name: 'Vocals',
            selected: {
              start: 2
            },
            start: 2
          }
        ])
        .then(function () {
          // can do stuff with the playlist.
          // const el = document.getElementsByClassName('waveform')
          // console.log('main: ', el[0])
          // el[0].classList.add('bg-waveform')
          const playlistOverplay = document.getElementsByClassName('playlist-overlay')
          // background-image: url(/media/img/track1.jpg);
          playlistOverplay[0].style.backgroundImage = "url('/media/img/track1.jpg')"
          playlistOverplay[1].style.backgroundImage = "url('/media/img/track2.jpg')"
        })
    },
    methods: {
      pause: () => {
        console.log('this is pause!')
        ee.emit('pause')
      },
      start: () => {
        console.log('this is play!')
        ee.emit('play')
      },
      stop: () => {
        console.log('this is stop!')
        ee.emit('stop')
      }
    }
  }
</script>

<style lang='scss' scoped>
  // @import '../assets/styles/playlist.scss';
  .bg-waveform {
    background-color: red;
  }
</style>
