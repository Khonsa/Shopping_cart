<template>
    <table class="table table-hover">
        <thead :class="theadColor">
        <tr>
            <th>Name</th>
            <th>Description</th>
            <th>Stock</th>
            <th>Price</th>
            <th>  </th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in listProduct" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.description }}</td>
            <td>{{ item.stock }}</td>
            <td>{{ item.price }}</td>
            <td>
                <button-comp @emitClick="addCart(index)" text="Add to Cart" class="add" warna="biruMuda"/> 
            </td>
        </tr>
        </tbody>
    </table>
  
</template>

<script>
export default {
    props:{
        listProduct:{
            type: Array,
            default: () => {
                return[]
            }
        },
        theadColor:{
            type: String,
            default: ""
        }

    },
    methods:{
        addCart(index){
            this.$emit('emitAdd', index)
            }
    }

}
</script>

<style>

.kuning{
    background-image: linear-gradient(to right, #E98230 ,  #F0D217);
    color: #251812;
}
</style>