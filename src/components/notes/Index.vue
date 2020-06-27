<template>
  <ol>
    <li v-for="note in notes">
      <pre>
        {{note | json}}
      </pre>
    </li>
  </ol>
</template>

<script>
import Firebase from 'firebase'

export default {
    data () {
        return {
            notes: []
        }
    },
    ready () {
        let firebase = new Firebase('https://keeper-e7dd6.web.app/')
        firebase.child('notes').on('child_added', (snapshot) => {
            let note = snapshot.val()
            this.notes.unshift(note)
        })
    }
}
</script>

<style>

</style>