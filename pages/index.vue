<template>
  <div>
    <div class="bghero">
      <div class="container mx-auto px-4 pt-40">
        <div class="flex">
          <div class="md:w-3/5">
            <div class="sizing-video">
              <div class="video-container collapsed show-play">
                <div class="video">
                  <video autoplay loop width="100%">
                    <source src="~/assets/1080p.mp4" type="video/mp4" />
                  </video>
                  <div class="play">></div>
                </div>
              </div>
            </div>
          </div>
          <div class="md:w-2/5">
            <h1 class="text-6xl font-bold pt-40 pb-80">
              Happy Birthday <br />
              <div class="text-9xl flex">
                <span class="text-blue-400">M</span>
                <span class="text-yellow-400">o</span>
                <span class="text-green-400">n</span>
                <span class="text-purple-400">i</span>
                <span class="text-gray-400">k</span>
                <span class="text-red-400">a</span>
              </div>
            </h1>
          </div>
        </div>
      </div>
    </div>

    <div class="py-40 bg-gray-100">
      <div class="container mx-auto px-5">
        <h2 class="text-5xl text-purple-700 font-bold text-center pb-10">
          Birthday wishes from friends
        </h2>
        <div class="grid grid-cols-5 gap-5 mb-10">
          <div class="col-span-2">
            <img
              class="item bg-white rounded-lg shadow-xl"
              src="/rakshu.jpeg"
              alt=""
            />
          </div>
          <div class="col-span-3">
            <img
              class="item bg-white rounded-lg shadow-xl"
              src="/akki.jpeg"
              width="100%"
              alt=""
            />
          </div>
        </div>
        <vue-masonry-wall
          :items="messages"
          :options="{ width: 600, padding: 12 }"
          :ssr="{ columns: 2 }"
        >
          <template v-slot:default="{ item }">
            <div class="item bg-white p-10 rounded-lg shadow-xl">
              <p class="text-2xl text-gray-600">{{ item.text }}</p>
              <h5 class="text-right mt-5 text-2xl font-semibold text-blue-600">
                - {{ item.author }}
              </h5>
            </div>
          </template>
        </vue-masonry-wall>
      </div>
    </div>
    <div class="container mx-auto px-4 pt-32 pb-40" v-if="showCarousel">
      <h2 class="text-5xl text-pink-700 font-bold text-center pb-10">
        Memories from the past...
      </h2>
      <client-only>
        <carousel-3d
          :controls-visible="true"
          :controls-prev-html="'<span class=\'text-gray-200 font-black text-8xl ml-10\'>&#10092;</span>'"
          :controls-next-html="'<span class=\'text-gray-200 font-black text-8xl mr-10\'>&#10093;</span>'"
          :controls-width="30"
          :controls-height="60"
          :autoplay="true"
          :autoplay-timeout="5000"
          :display="3"
          :width="800"
          :height="500"
        >
          <slide v-for="(slide, i) in slides" :index="i" :key="i">
            <img
              alt="Example image"
              :src="'/IMG_' + parseInt(i + 1) + '.jpg'"
              width="100%"
            />
          </slide>
        </carousel-3d>
      </client-only>
    </div>
  </div>
</template>

<script>
import VueMasonryWall from 'vue-masonry-wall'
export default {
  data() {
    return {
      slides: 20,
      showCarousel: false,
      messages: [
        {
          author: 'Girika',
          text:
            'Many many happy returns of the day darling🎂🎈🎉..Stay blessed 😁...Enjoy your day 😁😘😘😘',
        },
        {
          author: 'Ashwin Soman',
          text:
            'Happy Birthday Moni! With all the love your heart can hold, And the utter joy birthdays bring, May you have a truly special day, You deserve the best of everything. God bless 😇',
        },
        {
          author: 'Harshu',
          text:
            'Today is the birthday of the person who is spreading joy and positivity all around. May your birthday and life be as wonderful as you are..Happy Birthday',
        },
        {
          author: 'Khushboo',
          text:
            'Wish you never-ending bliss on your birthday. Be who you are, because who you are is amazing. Happyyy Birthday Monika!! 🤩🤩🎊🎊🎉🎉',
        },
        {
          author: 'Jagdeep',
          text:
            'Wish you a very very happppy birthday, you are one of the sweetest girl i have ever met, i miss our opus partiesss alot, jaldi se vapis aake saaala dhmaakedaar  herbal party karenge Dost 😜, again wish you a very Happy Birthday Monika.',
        },
        {
          author: 'Diptesh',
          text:
            "I'm neither good with cakes, nor cards, nor handicrafts, but let each word of mine symbolise the immense love and reverence that I have for you. Let this date mark the start of abundant joy and success for us both. Happy B'Day!!",
        },
        {
          author: 'Rajeev',
          text: 'Facebook told me that it’s your bday today, there you go! HBD',
        },
      ],
    }
  },
  components: { VueMasonryWall },
  mounted() {
    this.showCarousel = true
    var videoContainer = document.querySelector('.video-container'),
      video = videoContainer.querySelector('.video'),
      player = video.querySelector('video'),
      videoCaption = document.querySelector('.video-caption'),
      scrollOffset,
      SCROLL_COLLAPSE_THRESHOLD = 150,
      LG_VIEWPORT_WIDTH = 1040,
      TRANSITION_DURATION = 400,
      hasAutoplayed = !1
    window.addEventListener('resize', function () {
      updateVideoForViewportSize()
    }),
      player.addEventListener('play', function () {
        videoContainer.classList.remove('show-play')
      }),
      player.addEventListener('pause', function () {
        videoContainer.classList.add('show-play')
      })
    var autoplayVideo = function () {
        !hasAutoplayed &&
          video.getBoundingClientRect().top < window.innerHeight - 100 &&
          ((hasAutoplayed = !0), player.play())
      },
      updateVideoForViewportSize = function () {
        isLargeViewport()
          ? (isCollapsed() && hideControls(), (player.volume = 0))
          : ((video.style.transform = ''), collapseVideo(), showControls())
      }
    window.addEventListener('scroll', function () {
      autoplayVideo(),
        Math.abs(window.scrollY - scrollOffset) > SCROLL_COLLAPSE_THRESHOLD &&
          collapseVideo()
    }),
      autoplayVideo()
    var setVolume = function (e, t) {
        var n = function (e, t, n, r) {
            return (n * e) / r + t
          },
          r,
          i = player.volume,
          s = function (o) {
            r = r || o
            var u = o - r,
              a = n(u, i, e - i, t)
            ;(player.volume = a),
              u < t ? requestAnimationFrame(s) : (player.volume = e)
          }
        requestAnimationFrame(s)
      },
      showControls = function () {
        player.setAttribute('controls', 'true')
      },
      hideControls = function () {
        player.removeAttribute('controls')
      },
      isLargeViewport = function () {
        return window.innerWidth >= LG_VIEWPORT_WIDTH
      },
      isCollapsed = function () {
        return videoContainer.classList.contains('collapsed')
      },
      updateFullsizeVideoBounds = function () {
        var e = videoContainer.getBoundingClientRect().top,
          t = (window.innerHeight - video.offsetHeight) / 2 - e
        video.style.transform = 'translateY(' + t + 'px)'
      },
      expandVideo = function () {
        isCollapsed() &&
          (setVolume(1, 1500),
          player.play(),
          showControls(),
          video.classList.add('animated'),
          updateFullsizeVideoBounds(),
          (scrollOffset = window.scrollY),
          videoContainer.classList.remove('collapsed'),
          videoCaption.classList.remove('visible'),
          setTimeout(function () {
            video.classList.remove('animated')
          }, TRANSITION_DURATION))
      },
      collapseVideo = function () {
        isCollapsed() ||
          (setVolume(0, 0),
          player.pause(),
          hideControls(),
          video.classList.add('animated'),
          videoContainer.classList.add('collapsed'),
          videoCaption.classList.add('visible'),
          setTimeout(function () {
            video.classList.remove('animated')
          }, TRANSITION_DURATION))
      }
    document.addEventListener('click', function (e) {
      !isCollapsed() &&
        e.target != video &&
        window.innerWidth >= LG_VIEWPORT_WIDTH &&
        collapseVideo()
    }),
      video.addEventListener('click', function (e) {
        isLargeViewport() &&
          (e.stopPropagation(), isCollapsed() && expandVideo())
      }),
      updateVideoForViewportSize()
  },
}
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
.bghero {
  background-image: url('~assets/bg.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  color: white;
}
.sizing-video {
  position: relative;
  margin-top: -400px;
  margin-left: ;
}

.spacer-video {
  margin-top: 80px;
}

.video-container {
  position: relative;
  margin-top: 50px;
  z-index: 1;
  pointer-events: none;
}

@media (min-width: 670px) {
  .video-container {
    max-width: 100%;
  }
}

@media (min-width: 959px) {
  .video-container {
    position: absolute;
    width: 100%;
    max-width: none;
    top: 0;
    left: 0;
    perspective: 1200px;
    perspective-origin: 80% 80%;
    z-index: 1000;
  }
}

@media (min-width: 959px) {
  .video-container.collapsed .video {
    cursor: pointer;
    transform: scale(0.95) rotateX(-2deg) rotateY(15deg) rotate(1deg)
      translateX(10px) translateY(370px) !important;
    /*margin-left: 100px;*/
    /*margin-top: -20px;*/
  }

  .video-container.collapsed .video video {
    border-radius: 14px;
  }
}

@media (min-width: 959px) {
  .video-container.collapsed.show-play .play {
    opacity: 1;
  }
}

.video-container .video {
  position: relative;
  pointer-events: all;
  border-radius: 12px;
  box-shadow: 0 55px 70px -20px rgba(50, 50, 93, 0.55),
    0 20px 30px -10px rgba(0, 0, 0, 0.14);
}

@media (min-width: 959px) {
  .video-container .video.animated {
    transition: transform 0.4s cubic-bezier(0.645, 0, 0.355, 1);
  }
}

.video-container .video:hover .play {
  transform: scale(1.1);
}

.video-container .video:active .play {
  transform: none;
}

.video-container .video video {
  background-color: #32325d;
  display: block;
  position: relative;
  border-radius: 6px;
  -webkit-mask-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAIAAACQd1PeAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAA5JREFUeNpiYGBgAAgwAAAEAAGbA+oJAAAAAElFTkSuQmCC);
  transition: border-radius 0.4s cubic-bezier(0.645, 0, 0.355, 1);
}

.video-container .video .play {
  display: -ms-flexbox;
  display: flex;
  -ms-flex-align: center;
  align-items: center;
  -ms-flex-pack: center;
  justify-content: center;
  position: absolute;
  width: 120px;
  height: 120px;
  top: 50%;
  margin-top: -60px;
  left: 50%;
  margin-left: -60px;
  border-radius: 50%;
  background-color: hsla(0, 0%, 100%, 0.5);
  opacity: 0;
  transform-style: preserve-3d;
  pointer-events: none;
  /* background-image: url(../img/icons/play.svg); */
  background-position: calc(50% + 4px) 50%;
  background-repeat: no-repeat;
  transition: opacity 0.4s cubic-bezier(0.645, 0, 0.355, 1),
    transform 0.15s cubic-bezier(0.645, 0, 0.355, 1);
}

.video-caption {
  position: relative;
  margin-top: 30px;
  font-style: italic;
}

@media (min-width: 670px) {
  .video-caption {
    text-align: center;
  }
}

@media (min-width: 959px) {
  .video-caption {
    -ms-flex-preferred-size: 50%;
    flex-basis: 50%;
    margin-top: 430px;
    padding-left: 20px;
    padding-right: 40px;
    text-align: left;
    opacity: 0;
    transform: scale(0.95);
    transition: opacity 0.4s cubic-bezier(0.645, 0, 0.355, 1),
      transform 0.4s cubic-bezier(0.645, 0, 0.355, 1);
  }
}

.video-caption.visible {
  opacity: 1;
  transform: none;
}
.uk-close {
  display: inline-block;
  text-indent: -9999px;
  /* background: url(../img/icons/close.svg); */
  width: 24px;
  height: 24px;
  background-size: 24px 24px;
  position: absolute;
  top: 20px;
  right: 20px;
  opacity: 1;
}

@media (max-width: 959px) {
  .sizing-video {
    margin-top: 0px;
  }
}
</style>
