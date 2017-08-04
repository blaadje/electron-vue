<template lang="pug">
.root
  .connexion(v-if="showConnection")
    .content
      h1 Entrez votre nom d'utilisateur
      input(type="text", v-model="user", @keydown.enter="sendUser")
      button(@click.prevent="sendUser") Quitter
  .userList
    transition-group(name="fade", tag="ul")
      li(v-for="(user, index) in users", key="index") {{ username }} : {{ user.message }}
        button(@click.prevent="deleteUser(user)") X
    input(type="text", ref="message", @keydown.enter="addUser")
</template>

<script>
import Firebase from 'firebase'

var i = 0

var config = {
  databaseURL: 'https://projet-tets.firebaseio.com',
  projectId: 'projet-tets'
}
var firebaseApp = Firebase.initializeApp(config)
var db = firebaseApp.database()
var ref = db.ref('users')

export default {
  data () {
    return {
      user: '',
      showConnection: true,
      content: ''
    }
  },
  firebase () {
    return {
      users: ref.orderByKey()
    }
  },
  computed: {
    username () {
      return this.user.name === this.user ? 'moi' : this.user.name
    }
  },
  methods: {
    sendUser () {
      this.showConnection = false
    },
    addUser () {
      i++
      ref.child(this.getkey()).set({ message: this.$refs.message.value, name: this.user })
      this.$refs.message.value = ''
    },
    deleteUser (name) {
      ref.child(name['.key']).remove()
    },
    getkey () {
      var date = new Date()
      var yy = date.getFullYear()
      var mm = date.getMonth()
      var dd = date.getDay()
      var hh = date.getHours()
      var m = date.getMinutes()
      var s = date.getSeconds()

      mm = mm < 10 ? '0' + mm : mm
      dd = dd < 10 ? '0' + dd : dd
      hh = hh < 10 ? '0' + hh : hh
      m = m < 10 ? '0' + m : m
      s = s < 10 ? '0' + s : s

      let result = '-' + yy + '' + mm + '' + dd + '' + hh + '' + m + '' + s + i
      return result
    }
  }

}
</script>

<style lang="sass" src="./MyComponent.sass"></style>
