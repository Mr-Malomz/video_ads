<template>
  <div class="flex flex-col items-center p-8">
    <h1 class="text-xl font-medium text-blue-900 mb-8">Cloudinary Video Ads</h1>
    <div class="relative">
      <video :id="`video-player`" class="w-96 h-96" muted controls></video>
      <div
        v-if="showAds"
        class="flex justify-between w-96 py-4 px-4 bg-white shadow-lg absolute bottom-0 z-10"
      >
        <section class>
          <p>Read more contents from</p>
          <a href="https://hackmamba.io/" target="_blank" class="font-medium text-blue-700">Here</a>
        </section>
        <button class="font-bold" @click="closeShowAds">X</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      cld: null,
      player: null,
      showAds: false,
      interval: null,
      timeRun: 0
    }
  },

  mounted() {
    this.player = this.videoList;

    this.cld = cloudinary.Cloudinary.new({
      cloud_name: process.env.NUXT_ENV_CLOUDINARY_CLOUD_NAME,
      secure: true,
    })

    this.player = this.cld.videoPlayer(`video-player`)

    this.player.source(`dancing-catvideo.jpg`)

    this.player.play()
  },

  methods: {
    closeShowAds() {
      this.showAds = false;
    },

    openShowAds() {
      this.showAds = true;
    },
  },

  created() {
    this.interval = setInterval(() => {
      this.timeRun += 1;
      if (this.timeRun === 10) {
        this.openShowAds()
      }
      if (this.timeRun === 20) {
        this.closeShowAds()
      }
    }, 1000);
  },

}
</script>