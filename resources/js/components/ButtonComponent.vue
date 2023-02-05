<template>
  <button type="button" class="btn" @click="emitClick" :class="warna">{{ text }}</button>
</template>

<script>
export default {
    props:{
        text:{
            type: String,
            default: ""
        },
        warna:{
            type: String,
            default: ""
        }
    },
    methods:{
        emitClick(){
            this.$emit('emitClick')
        }
    }

}
</script>

<style>
.biruMuda{
    background: #00A3E1;
    color: white;
}

.biruMuda:hover{
    background:#0B1C52;
    color:white;
    transition: 0.5s;
}

.merah{
    background: #DF1B22;
    color: white;
}

.merah:hover{
    background:#9E0E22;
    color:white;
    transition: 0.5s;
}

.hijau{
    background: #009C4D;
    color: white;
}

.hijau:hover{
    background:#003419;
    color:white;
    transition: 0.5s;
}

</style>