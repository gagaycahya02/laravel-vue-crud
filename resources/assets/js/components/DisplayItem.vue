<template>
    <div>
        <h1>Items</h1>

        <div class="row">
            <div class="col-md-10"></div>
            <div class="col-md-2">
                <router-link :to="{ name: 'CreateItem' }" class="btn btn-primary">Create Item</router-link>
            </div>
        </div><br>
        <table class="table table-hover">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Price</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="item in items" :key="item.id">
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                    <td>$ {{ item.price }}</td>
                    <td>
                        <router-link :to="{ name: 'EditItem', params: { id: item.id }}" class="btn btn-primary">Edit Item</router-link>
                        <button class="btn btn-danger" @click="deleteItem(item.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'DisplayItem',
        data(){
            return {
                items: []
            }
        },
        created(){
            this.fetchItems()
        },
        methods: {
            fetchItems() {
                let uri = 'http://localhost:8000/items'
                this.axios.get(uri).then((response) => {
                    this.items = response.data;
                })
            },
            deleteItem(id){
                let uri = `http://localhost:8000/items/${id}`
                let confirm = window.confirm("Remove this item ?")

                if(confirm){
                    this.items.splice(id, 1)
                    this.axios.delete(uri)
                    window.location.reload()
                }
            }
        }
    }
</script>

