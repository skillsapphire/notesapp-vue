<template>
    <div>
        <h1>Notes</h1>
        <div class="row">
            <div class="col-3">
                <button class="btn btn-primary" v-on:click="fetchItems('id','asc')">Sort by Id(asc)</button>
            </div>
            <div class="col-3">
                <button class="btn btn-primary" v-on:click="fetchItems('id','desc')">Sort by Id(desc)</button>
            </div>
            <div class="col-3">
                <button class="btn btn-primary" v-on:click="fetchItems('creationDate','asc')">Sort by creation date(asc)</button>
            </div>
            <div class="col-3">
                <button class="btn btn-primary" v-on:click="fetchItems('creationDate','desc')">Sort by creation date(desc)</button>
            </div>
        </div>
        <table class="table table-hover">
            <thead>
            <tr>
                <td>Note Id</td>
                <td>Note Title</td>
                <td>Note Content</td>
                <td>Created on</td>
                <td>Last updated</td>
            </tr>
            </thead>

            <tbody>
                <tr v-for="(item, index) in items" :key="item.id">
                    <td>{{ item.id }}</td>
                    <td>{{ item.title }}</td>
                    <td>{{ item.content }}</td>
                    <td>{{ item.createdAt }}</td>
                    <td>{{ item.lastModifiedAt }}</td>
                    <td><button class="btn btn-danger" v-on:click="deleteItem(index, item.id)">Delete</button></td>
                </tr>
                
            </tbody>
        </table>
    </div>
</template>

<script>

    export default {
        data(){
            return{
                items: []
            }
        },

        created: function()
        {
            this.fetchItems('creationDate','desc');
        },

        methods: {
            fetchItems(field, type)
            {
              let uri = 'https://notesv2.herokuapp.com/api/notes?field='+field+'&type='+type;
              //let uri = 'http://localhost:9090/api/notes/?field='+field+'&type='+type;
              this.axios.get(uri).then((response) => {
                  this.items = response.data;
              });
            },
            deleteItem(index, id)
            {
                let uri = 'https://notesv2.herokuapp.com/api/notes/'+id;
             // let uri = 'http://localhost:9090/api/notes/'+id;
              this.axios.delete(uri);
              this.items.splice(index, 1);
            }
        }
    }
</script>