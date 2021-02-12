<template>
  <div id="app">
    <p>
      <label>Let me guess your age by your name:
        <input v-model="name" @keyup="guessAge()" />
      </label>
    </p>
    <div v-if="!loading && name != ''">
      <h2>{{ name }}, are you {{ age }}?</h2>
      <p>There are {{ count }} people called "{{ name }}" with average age of {{ age }}.</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      name: '',
      age: 0,
      count: 0,
      loading: true
    }
  },
  methods: {
    guessAge() {
      if ( this.name !== '' ) {
        axios
          .get('https://api.agify.io/?name='+this.name)
          .then(response => {
            this.age = response.data.age
            this.count = response.data.count
          })
          .catch(error => {
            console.log(error)
          })
          .finally(() => this.loading = false)
      } else {
          this.loading = true
      }
    }
  }
}
</script>

<style>

</style>
