<template>
  <div class="app">
    <div class="app__main">
      <TheJoke v-if="joke"
        v-bind:joke="joke"
      />
      <p v-else-if="error">
        {{ error.message }}
      </p>
      <p v-else>
        Loading...
      </p>
      <JokeTools v-bind:joke="joke"
        v-on:copyLink="copyLink"
        v-on:getJoke="() => getJoke()"
      />
    </div>
    <div class="app__footer">
      <TheFooter />
    </div>
  </div>
</template>

<script>
import TheJoke from '@/components/TheJoke'
import JokeTools from '@/components/JokeTools'
import TheFooter from '@/components/TheFooter'

export default {
  name: 'App',
  components: {
    TheJoke,
    JokeTools,
    TheFooter
  },
  data () {
    return {
      error: null,
      joke: null
    }
  },
  methods: {
    async getJoke (id) {
      this.error = null
      this.joke = null

      let data

      const url = id
        ? `http://api.icndb.com/jokes/${id}`
        : 'http://api.icndb.com/jokes/random'

      try {
        const response = await fetch(url)
        data = await response.json()
      } catch (e) {
        this.error = e
        return
      }

      this.joke = data.value

      history.replaceState(this.joke, '', `/${this.joke.id}`)
    },

    onKeyDown (ev) {
      if (ev.which == 32) {
        this.getJoke()
      }
    },

    copyLink () {
      let input = document.createElement('input')
      document.body.appendChild(input)
      input.value = window.location.href
      input.select()
      document.execCommand('copy')
      document.body.removeChild(input)
      alert('Copied!')
    }
  },

  created () {
    if (window.location.pathname === '/') {
      this.getJoke()
      return
    }

    const matched = window.location.pathname.match(/^\/(\d+)$/)
    if (matched) {
      this.getJoke(matched[1])
      return
    }

    this.error = new Error("404")
  },

  mounted () {
    window.addEventListener('keydown', this.onKeyDown)
  },
  beforeDestroy () {
    window.removeEventListener('keydown', this.onKeyDown)
  }
}
</script>

<style>
.app {
  padding: 0 10vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.app__main {
  margin: auto;
}
.app__footer {
  margin: auto;
}
</style>
