<template>
  <section class="container">
    <div>
      <app-logo/>
        <h1 class="title">
          nuxt-trans-demo
        </h1>
      <h2 class="subtitle">
        Countries
      </h2>
      <ul>
        <li v-for="(country,index) in countries" :key="index">
          {{ $t(country.Title) }} ||
          <span v-if="disease" style="color: red" v-for="(disease,index) in country.collectionlink" :key="index">
            {{disease.display}}
           </span>
          </li>
      </ul>
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
import axios from 'axios'

export default {
   asyncData({ req, params }) {
    // We can return a Promise instead of calling the callback
    return axios.get('http://localhost/demos/nuxt-trans-demo/cms/api/collections/get/Countries/posts?token=5d748a0c3d5cccb912e82a29bb7169')
      .then((res) => {
        console.log(res.data)
        return { countries: res.data.entries }
      })
  },
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
  }//transition
}
</script>

<style scoped>
  .container {
    background-color: darkslategray;
  }
</style>
