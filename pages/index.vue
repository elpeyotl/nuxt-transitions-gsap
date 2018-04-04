<template>
  <section class="container">
    <div>
      <app-logo/>
        <h1 class="title">
          nuxt-trans-demo
        </h1>
      <h2 class="subtitle">
        Nuxt.js project
      </h2>
      <div class="links">
        <nuxt-link to="/about">
          <button class="button--green">
            About
          </button>
        </nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'
import { TweenLite} from 'gsap'

export default {
  components: {
    AppLogo
  },
   transition: {
    mode: 'out-in',
    css: false,
    beforeEnter (el, done) {
      TweenMax.from('h1', 1, {
         ease: Back.easeInOut, x: "400%", opacity: 0, onComplete: done
      })
      TweenMax.from('.subtitle', 1, {
         ease: Back.easeInOut, x: "-400%", opacity: 0
      })
      TweenMax.from(el, 1, {
         opacity: 0
      })
    },
    leave (el, done) {
       TweenMax.to('h1', 1, {
         ease: Back.easeInOut, x: "400%", opacity: 0, onComplete: done
      }),
       TweenMax.to('.subtitle', 1, {
         ease: Back.easeInOut, x: "-400%", opacity: 0
      })
      TweenMax.to(el, 1, {
        opacity: 0
      })
    }
  }
}
</script>

<style scoped>
  .container {
    background-color: darkslategray;
  }
</style>
