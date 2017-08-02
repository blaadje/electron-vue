<template lang="pug">
  .userList
    transition-group(name="fade", tag="ul")
      li(v-for="(user, index) in users", key="index") {{ user.name }}
        button(@click.prevent="deleteUser(user)") X
    input(type="text", ref="name", @keydown.enter="addUser")
</template>

<script>
import Firebase from 'firebase'

var config = {
  apiKey: 'AIzaSyBz73_KOl_AYMfeJnBQ7lBCyH-KuSUQsqQ',
  authDomain: 'projet-tets.firebaseapp.com',
  databaseURL: 'https://projet-tets.firebaseio.com',
  projectId: 'projet-tets',
  storageBucket: 'projet-tets.appspot.com',
  messagingSenderId: '304277615671'
}
var firebaseApp = Firebase.initializeApp(config)
var db = firebaseApp.database()

export default {
  firebase () {
    return {
      users: db.ref('users')
    }
  },
  created () {
    return {
      users: db.ref('users')
    }
  },
  methods: {
    addUser () {
      this.newUser = this.$refs.name.value
      db.ref('users').push({ name: this.$refs.name.value })
      this.$refs.name.value = ''
    },
    deleteUser (name) {
      db.ref('users').child(name['.key']).remove()
    }
  }

}
</script>

<style lang="sass">
.userList
  ul
    margin: 0
    padding: 0
    li
      transition: transform 1s ease
      list-style-type: none
      padding: 1em
      &:not(:last-child)
        border-bottom: 1px solid grey
      &.fade-enter
        transform: translateX(-400px)
      &.fade-enter-to
        transform: translateX(0)
      &.fade-leave-to
        transform: translate(-400px)
</style>
