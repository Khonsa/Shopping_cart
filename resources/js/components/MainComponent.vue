<template>
    <div class="container">
        <div class="product">
            <title-comp styleTitle="underlineStyle" teks="Semua Produk"/>
            <product :listProduct="list" @emitAdd="addCart" @emitAddAll="addAll" theadColor="kuning"/>
        </div>

        <div class="cart">
            <title-comp styleTitle="commonStyle backgndJudul" teks="Keranjang Belanja"/>
            <div class="isiCart">
                <p> Jika sudah selesai berbelanja silahkan klik tombol checkout untuk membayar</p>
                <cart :dataCart="listcart" @deleteElement="deleteCart" @delOneElement="delOne"/>
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
                    price: 3900
                },
                {
                    name: "Mie Gelas Rendang",
                    description : "Mie instan khusus anak kosan",
                    stock: 3,
                    price: 1500
                },
                {
                    name: "Bakmi Mewah",
                    description : "Kalau anak kosan jangan macam2 deh",
                    stock: 80,
                    price: 10000
                }],
                listcart:[]
            }
        },
        methods:{
            addCart(index){
                    var id_add = document.getElementsByClassName("add")[index]
                    var id_all = document.getElementsByClassName("all")[index]
                    if (this.list[index].stock > 0){
                        this.list[index].stock -=  1
                        if (this.listcart.find((listcartData) => listcartData.name === this.list[index].name)){
                            let indexListcart = this.listcart.map(ind => ind.name).indexOf(this.list[index].name)
                            let pricelist = this.list[index].price
                            let pricecart = this.listcart[indexListcart].price
                            this.listcart[indexListcart].quantity = this.listcart[indexListcart].quantity + 1
                            this.listcart[indexListcart].price = pricecart + pricelist
                        }else{
                            let newlistcart = {
                            name : this.list[index].name,
                            quantity : 1,
                            price : this.list[index].price}
                            this.listcart.push(newlistcart);
                        }
                        if (this.list[index].stock == 0){
                            id_add.style.visibility = "hidden"
                            id_all.style.visibility = "hidden"
                        }else{
                            id_add.style.visibility = "visible"
                            id_all.style.visibility = "visible"
                        }
                    }else{
                        this.list[index].stock = 0
                    }

                    let total_bayar = 0
                    for (let i = 0; i < this.listcart.length; i++) {
                        total_bayar = total_bayar + this.listcart[i].price;
                    }
                    document.getElementById("total").innerHTML = "Rp. " + total_bayar
            },
            addAll(index){
                    /*deklarasi class button = all dan add*/
                    var id_all = document.getElementsByClassName("all")[index]
                    var id_add = document.getElementsByClassName("add")[index]
                    /*deklarasi harga dari tabel list ke type number*/
                    let pricelist = this.list[index].price
                    /*Cek tabel listcartnya ada data atau tidak*/
                    if (this.list[index].stock > 0){
                        /*Kalau adat data cari kolom nama dari tabel listcart yg sama dgn tabel list*/
                        if (this.listcart.find((listcartData) => listcartData.name === this.list[index].name)){
                            let indexListcart = this.listcart.map(ind => ind.name).indexOf(this.list[index].name)
                            let pricecart = this.listcart[indexListcart].price
                            this.listcart[indexListcart].quantity = this.listcart[indexListcart].quantity + this.list[index].stock
                            this.listcart[indexListcart].price = pricecart + pricelist
                            this.list[index].stock = 0
                        }else{
                            /*Kalau tidak ada tambah data baru pada tabel listcart*/
                            let newlistcart = {
                            name : this.list[index].name,
                            quantity : this.list[index].stock,
                            price : this.list[index].stock * pricelist
                            }
                            this.listcart.push(newlistcart)
                            this.list[index].stock = 0
                        }
                        if (this.list[index].stock == 0){
                            id_all.style.visibility = "hidden"
                            id_add.style.visibility = "hidden"
                        }else{
                            id_all.style.visibility = "visible"
                            id_add.style.visibility = "visible"
                        }
                    }else{
                        this.list[index].stock = 0
                    }
                    let total_bayar = 0
                    for (let i = 0; i < this.listcart.length; i++) {
                        let dataPriceCart = this.listcart[i].price
                        total_bayar = total_bayar + dataPriceCart
                    }
                    document.getElementById("total").innerHTML = "Rp. " + total_bayar
            },
            deleteCart(index){
                let indexList = this.list.map(ind => ind.name).indexOf(this.listcart[index].name)
                this.list[indexList].stock += this.listcart[index].quantity
                let tot_temp = Number(document.getElementById("total").innerHTML.replace('Rp. ',''))
                tot_temp -= this.listcart[index].price
                document.getElementById("total").innerHTML = "Rp. " + tot_temp
                this.listcart.splice(index,1)
                var id_add = document.getElementsByClassName("add")[indexList]
                var id_all = document.getElementsByClassName("all")[indexList]
                if (id_add.style.visibility = "hidden"){
                    id_add.style.visibility = "visible"
                    id_all.style.visibility = "visible"
                }
            },
            delOne(index){
                let indexList = this.list.map(ind => ind.name).indexOf(this.listcart[index].name)
                this.list[indexList].stock += 1
                this.listcart[index].quantity -= 1
                this.listcart[index].price -= this.list[indexList].price
                let tot_temp = Number(document.getElementById("total").innerHTML.replace('Rp. ',''))
                tot_temp -= this.list[indexList].price
                document.getElementById("total").innerHTML = "Rp. " + tot_temp
                if (this.listcart[index].quantity == 0){
                    this.listcart.splice(index,1)
                }
                var id_add = document.getElementsByClassName("add")[indexList]
                var id_all = document.getElementsByClassName("all")[indexList]
                if (id_add.style.visibility = "hidden"){
                    id_add.style.visibility = "visible"
                    id_all.style.visibility = "visible"
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
