<template>
    <div>Delete vue</div>
</template>
<script>
export default {
  data() {
      return {
          item: {}
      }
  },
  methods: {
      deleteNotes(noteId) {
           let uri = 'https://notesv2.herokuapp.com/api/notes/{}';
            this.axios.post(uri, this.item).then((response) => {
                console.log(response.data)
            });
        }
    }
}
</script>