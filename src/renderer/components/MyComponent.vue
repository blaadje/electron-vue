<template lang="pug">
.root
  .connexion(v-if="showConnection === true")
    .content
      h1 Entrez votre nom d'utilisateur
      input(type="text", v-model="user")
      button(@click.prevent="showConnection = false") Quitter
  .userList
    span {{ user }}
    transition-group(name="fade", tag="ul")
      li(v-for="(user, index) in users", key="index") {{ user.name }}
        p {{ user['.key'] }}
        button(@click.prevent="deleteUser(user)") X
    input(type="text", ref="name", @keydown.enter="addUser")
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
  methods: {
    addUser () {
      i++
      this.newUser = this.$refs.name.value
      ref.child(this.getkey()).set({ name: this.$refs.name.value })
      this.$refs.name.value = ''
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
