<template>
    <div>
        <h1>Update item</h1>

        <div class="row">
            <div class="col-md-10"></div>
            <div class="col-md-2">
                <router-link :to="{ name: 'DisplayItem' }" class="btn btn-primary">Return to item</router-link>
            </div>
        </div>

        <div class="row">
            <div class="col-md-5">
                <form @submit.prevent="updateItem">
                    <div class="form-group">
                        <label>Item name :</label>
                        <input type="text" class="form-control" v-model="item.name">
                    </div>

                    <div class="form-group">
                        <label>Item price :</label>
                        <input type="text" class="form-control" v-model="item.price">
                    </div>

                    <div class="form-group">
                        <button class="btn btn-primary">Update Item</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'EditItem',
        data() {
            return {
                item: {}
            }
        },
        created (){
            this.getItem()
        },
        methods : {
            getItem() {
                let uri = `http://localhost:8000/items/${this.$route.params.id}/edit`
                this.axios.get(uri).then((response) => {
                    this.item = response.data
                })
            },
            updateItem() {
                let uri = 'http://localhost:8000/items/'+this.$route.params.id
                this.axios.patch(uri, this.item).then((response) => {
                    this.$router.push({ name: 'DisplayItem' })
                })
            }
        }
    }   
</script>

