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
            <td>Rp. {{ item.price }}</td>
            <td>
                <button-comp @emitClick="deleteOne(index)" text="-1" warna="merah"/>
                <button-comp @emitClick="deleteCart(index)" text="Delete All" warna="merah"/>
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
            },
        deleteOne(index){
            this.$emit('delOneElement', index)
            }
    }
}
</script>

<style>

</style>