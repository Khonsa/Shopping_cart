<template>
    <div class="container">
        <div class="product">
            <h1>Semua Produk</h1>
            <table class="table">
                <thead>
                <tr>
                    <th>Name</th>
                    <th>Description</th>
                    <th>Stock</th>
                    <th>Price</th>
                    <th>  </th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(item, index) in list" :key="index">
                    <td>{{ item.name }}</td>
                    <td>{{ item.description }}</td>
                    <td>{{ item.stock }}</td>
                    <td>{{ item.price }}</td>
                    <td>
                    <button type="button" class="btn btn-primary add" @click="addCart(index)">Add to cart</button>
                    </td>
                </tr>
                </tbody>
            </table>
        </div>
        <div class="cart">
            <h1>Keranjang Belanja</h1>
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
                <tr v-for="(item, index) in listcart" :key="index">
                    <td>{{ item.name }}</td>
                    <td>{{ item.quantity }}</td>
                    <td>{{ item.price }}</td>
                    <td>
                    <button class="btn btn-danger" @click="deleteCart(index)">Delete</button>
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
            <button class="btn btn-success" @click="checkout()">Checkout</button>
        </div>
    </div>
</template>

<script>
    export default {
        data: function(){
            return{
                list:[{
                    name: "Indomie Goreng Rendang",
                    description : "Masakan instan terenak di dunia",
                    stock: 10,
                    price: "Rp. 3900"
                },
                {
                    name: "Mie Gelas Rendang",
                    description : "Mie instan khusus anak kosan",
                    stock: 3,
                    price: "Rp. 1500"
                },
                {
                    name: "Bakmi Mewah",
                    description : "Kalau anak kosan jangan macam2 deh",
                    stock: 80,
                    price: "Rp. 10000"
                }],
                listcart:[]
            }
        },
        methods:{
            addCart(index){
                    var id_add = document.getElementsByClassName("add")[index]
                    if (this.list[index].stock > 0){
                        this.list[index].stock -=  1
                        if (this.listcart.find((listcartData) => listcartData.name === this.list[index].name)){
                            let indexListcart = this.listcart.map(ind => ind.name).indexOf(this.list[index].name)
                            let pricelist = Number(this.list[index].price.replace('Rp. ',''))
                            let pricecart = Number(this.listcart[indexListcart].price.replace('Rp. ', ''))
                            this.listcart[indexListcart].quantity = this.listcart[indexListcart].quantity + 1
                            this.listcart[indexListcart].price = 'Rp. ' + String(pricecart + pricelist)
                        }else{
                            let newlistcart = {
                            name : this.list[index].name,
                            quantity : 1,
                            price : this.list[index].price}
                            this.listcart.push(newlistcart);
                        }
                        if (this.list[index].stock == 0){
                            id_add.style.visibility = "hidden"
                        }else{
                            id_add.style.visibility = "visible"
                        }
                    }else{
                        this.list[index].stock = 0
                    }

                    let total_bayar = 0
                    for (let i = 0; i < this.listcart.length; i++) {
                        total_bayar = total_bayar + Number(this.listcart[i].price.replace('Rp. ',''));
                    }
                    document.getElementById("total").innerHTML = "Rp. " + total_bayar
            },
            deleteCart(index){
                let indexList = this.list.map(ind => ind.name).indexOf(this.listcart[index].name)
                console.log(indexList)
                this.list[indexList].stock += this.listcart[index].quantity
                let tot_temp = Number(document.getElementById("total").innerHTML.replace('Rp. ',''))
                tot_temp -= Number(this.listcart[index].price.replace('Rp. ',''))
                console.log(tot_temp)
                document.getElementById("total").innerHTML = "Rp. " + tot_temp
                this.listcart.splice(index,1)
                var id_add = document.getElementsByClassName("add")[indexList]
                if (id_add.style.visibility = "hidden"){
                    id_add.style.visibility = "visible"
                }
            },
            checkout(){
                swal({
                    title: "Yakin dengan belanjaanmu?",
                    text: "Silahkan membayar " + document.getElementById("total").innerHTML + " ! batalkan jika masih ragu.",
                    icon: "warning",
                    buttons: {
                        cancel : "Batal", 
                        Bayar : true},
                    })
                    .then((jadiBayar) => {
                        if (jadiBayar) {
                            swal("Terimakasih, Pembayaran belanjaanmu berhasil!", {
                                icon: "success",
                            });
                        } else {
                            swal("Silahkan dicek kembali belanjaannya");
                        }
                });
            }
        },
        mounted() {
            console.log('Component mounted.')
        }
    }
</script>
