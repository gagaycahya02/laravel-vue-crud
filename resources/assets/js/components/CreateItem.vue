<template>
    <div>
        <h1>Create an item</h1>
    
        <form @submit.prevent="addItem">
            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Item name: </label>
                        <input type="text" class="form-control" v-model="item.name"/>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <label>Item price : </label>
                        <input type="text" class="form-control" v-model="item.price"/>
                    </div>
                </div>
            </div>

            <div class="row">
                <div class="col-md-6">
                    <div class="form-group">
                        <button class="btn btn-primary">Add Item</button>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'CreateItem',
        data(){
            return {
                item: {}
            }
        },
        methods: {
            addItem(){
                let uri = 'http://localhost:8000/items'
                this.axios.post(uri,this.item).then((response) => {
                    this.$router.push({ name: 'DisplayItem' })
                })
            }
        }
    }
</script>

