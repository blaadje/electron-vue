<template lang="pug">
  .userList
    transition-group(name="fade", tag="ul")
      li(v-for="(user, index) in users", key="index") {{ user.name }}
        p {{ user['.key'] }}
        button(@click.prevent="deleteUser(user)") X
    input(type="text", ref="name", @keydown.enter="addUser")
</template>

<script>
import Firebase from 'firebase'

var config = {
  databaseURL: 'https://projet-tets.firebaseio.com',
  projectId: 'projet-tets'
}
var firebaseApp = Firebase.initializeApp(config)
var db = firebaseApp.database()
var ref = db.ref('users')

export default {
  firebase () {
    return {
      users: ref.orderByKey()
    }
  },
  methods: {
    addUser () {
      this.newUser = this.$refs.name.value
      // db.ref('users').push({ name: this.$refs.name.value })
      ref.child(this.getkey()).set({ name: this.$refs.name.value })
      this.$refs.name.value = ''
    },
    deleteUser (name) {
      ref.child(name['.key']).remove()
    },
    getkey () {
      // let key = Math.random().toString(36).substring(3)
      let date = new Date()
      let yy = date.getFullYear()
      let mm = date.getMonth()
      let dd = date.getDay()
      let m = date.getMinutes()
      let s = date.getSeconds()
      let result = '-' + yy + '' + mm + '' + dd + '' + m + '' + s
      return result
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
      list-style-type: none
      padding: 1em
      &:not(:last-child)
        border-bottom: 1px solid grey
      &.fade-active
        transition: transform 1s ease
      &.fade-enter
        transform: translateX(-400px)
      &.fade-enter-to
        transform: translateX(0)
      &.fade-leave-to
        transform: translate(-400px)
</style>
