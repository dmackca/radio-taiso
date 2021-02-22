<template>
  <div class="index page is-flex-direction-column" :class="pageClasses">
    <client-only placeholder="Loading...">
      <div class="video-wrap">
        <figure class="image is-16by9">
          <iframe
            class="has-ratio"
            width="640"
            height="360"
            :src="todayVideo"
            allow="autoplay"
            frameborder="0"
            allowfullscreen
          />
        </figure>
      </div>
    </client-only>
  </div>
</template>

<script>
import arrSample from 'lodash.sample'

export default {
  name: 'RadioTaiso',

  data: () => ({
    // videos for each day of the week
    videos: [
      // sunday
      ['UMkXEcJFE4k'],

      // monday
      [
        'XMOBmeESO4A',
        'UwYVSWrk-JE'
      ],

      // tuesday
      ['0xfDmrcI7OI'],

      // wednesday
      ['UMkXEcJFE4k'],

      // thursday
      ['0MYo07LeQ00'],

      // friday
      ['lgsh5vP54BM'],

      // saturday
      ['UMkXEcJFE4k']
    ]
  }),

  computed: {
    dayOfWeek () {
      return (new Date()).getDay()
    },

    dayVideos () {
      return this.videos[this.dayOfWeek]
    },

    todayVideo () {
      const videoId = arrSample(this.dayVideos)
      let url = `https://www.youtube.com/embed/${videoId}`

      if (this.$route.query.autoplay !== '0') {
        url += '?autoplay=1'
      }

      return url
    },

    pageClasses () {
      return [
        `day-${this.dayOfWeek}`
      ]
    }
  }
}
</script>

<style lang="scss">
@import '~bulma/sass/utilities/all';

.index.page {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: url('~/assets/bg/omoide.jpg') $white-ter;
  background-size: cover;

  .video-wrap {
    width: 100%;
    background: $black;
    box-shadow: 0 5px 30px rgba(0, 0, 0, 0.3);

    @include tablet {
      max-width: 80vw;
    }
  }
}
</style>
