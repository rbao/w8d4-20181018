<template>
  <div class="home">
    <h1>{{title}}</h1>
    <h4>{{fullName}}</h4>

    <a href="#">Random Link</a>

    <ul>
      <url-item v-for="url in urlDatabase" :url="url" @edit="editUrl"></url-item>
    </ul>

    <form @submit.prevent="submit">
      <p>
        <label>Name</label>
        <input v-model="name" type="text" name="name">
      </p>
      <p>
        <label>Long URL</label>
        <input v-model="longUrl" type="text" name="longUrl">
      </p>

      <button type="submit">Submit</button>
      <button v-if="isEditing" @click="cancelEdit" type="button" style="margin-left: 10px;">Cancel Edit</button>
    </form>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import UrlItem from '@/components/UrlItem.vue'

export default {
  name: 'home',
  components: {
    UrlItem
  },
  data: function () {
    return {
      firstName: 'Roy',
      lastName: 'Bao',
      title: 'TinyApp from State',
      name: '',
      longUrl: 'http://',
      isEditing: false,
      id: undefined,
      urlDatabase: [
        {
          id: 1,
          name: 'Google',
          longUrl: 'http://google.ca'
        },
        {
          id: 2,
          name: 'Facebook',
          longUrl: 'http://facebook.ca'
        }
      ]
    }
  },
  created: function () {
    setTimeout(() => {
      this.title = 'TINYAPP'
    }, 3000)
  },
  computed: {
    fullName () {
      return `${this.firstName} ${this.lastName}`
    }
  },
  methods: {
    cancelEdit () {
      this.isEditing = false
      this.name = ''
      this.longUrl = 'http://'
    },

    editUrl (urlObject) {
      this.firstName = 'Tom'
      this.isEditing = true
      this.id = urlObject.id
      this.name = urlObject.name
      this.longUrl = urlObject.longUrl
    },

    submit () {
      if (this.isEditing) {
        let targetId = this.id

        // 1. Find the target url
        let targetUrlObject = this.urlDatabase.find((url) => {
          return url.id === targetId
        })

        // 2. Update its attribute
        targetUrlObject.name = this.name
        targetUrlObject.longUrl = this.longUrl

      } else {
        let urlObject = {
          id: 3,
          name: this.name,
          longUrl: this.longUrl
        }

        this.urlDatabase.push(urlObject)
      }
    }
  }
}
</script>

<style>

</style>
