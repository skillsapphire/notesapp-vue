<template>
  <div class="container">
        <div class="card">
            <div class="card-header">
                <h3>Add Item</h3>
            </div>
            <div class="card-body">
                <form v-on:submit.prevent="addItem">
                    <div class="form-group">
                        <label>Note Title:</label>
                        <input type="text" class="form-control" v-model="item.title" placeholder="Note title"/>
                    </div>
                    <div class="form-group">
                        <label>Note Content:</label>
                        <input type="text" class="form-control" v-model="item.content" placeholder="Note content"/>
                    </div>
                    <div class="form-group">
                        <input type="submit" class="btn btn-primary" value="Add Item"/>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  data() {
      return {
          item: {}
      }
  },
  methods: {
      addItem() {
           let uri = 'https://notesv2.herokuapp.com/api/notes';
          // let uri = 'http://localhost:9090/api/notes/';
            this.axios.post(uri, this.item).then((response) => {
                console.log(response.data)
            });
        }
    }
}
</script>
