<template>
    <table class="table">
        <thead>
        <tr>
            <th>Name</th>
            <th>Quantity</th>
            <th>Price</th>
            <th>  </th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(item, index) in dataCart" :key="index">
            <td>{{ item.name }}</td>
            <td>{{ item.quantity }}</td>
            <td>{{ item.price }}</td>
            <td>
                <button-comp @emitClick="deleteCart(index)" text="Delete" warna="merah"/>
            </td>
        </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>Total:</td>
                <td> </td>
                <td id="total">Rp. 0</td>
            </tr>
        </tfoot>
    </table>
</template>

<script>
export default {
    props:{
        dataCart:{
            type: Array,
            default: () => {
                return[]
            }
        }
    },
    methods:{
        deleteCart(index){
            this.$emit('deleteElement', index)
            }
    }
}
</script>

<style>

</style>