<template>
    <div class="container">
        <div class="product">
            <title-comp styleTitle="underlineStyle" teks="Semua Produk"/>
            <product :listProduct="list" @emitAdd="addCart" theadColor="kuning"/>
        </div>

        <div class="cart">
            <title-comp styleTitle="commonStyle backgndJudul" teks="Keranjang Belanja"/>
            <div class="isiCart">
                <p> Jika sudah selesai berbelanja silahkan klik tombol checkout untuk membayar</p>
                <cart :dataCart="listcart" @deleteElement="deleteCart"/>
                <button-comp @emitClick="checkout" text="Checkout" warna="hijau"/>
            </div>
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
