<template>
  <div class="page-wrap">
  	<client-only>
  	  <div class="index page is-flex-direction-column" :class="pageClasses">
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
  	  </div>
  	  <template slot="placeholder">
  	    <div class="index page is-flex-direction-column placeholder">
  	        <div class="loading-message">🤹 Loading...</div>
  	    </div>
  	  </template>
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

  mounted() {
    console.log('today is: %s', this.dayOfWeek)
  },

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
  background: url('~/assets/bg/omoide.jpg') #9dba9c;
  background-size: cover;

  .video-wrap {
    $shadow-color: rgba(0, 0, 0, 0.8);

    width: 100%;
    background: $shadow-color;
    box-shadow: 0 5px 30px $shadow-color;

    @include tablet {
      max-width: 80vw;
      overflow: hidden;
      border-radius: 0.75rem;
    }
  }
}
</style>
