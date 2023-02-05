<template>
    <h1 type="text" :class="styleTitle">{{ teks }}</h1>
  </template>
  
  <script>
  export default {
      props:{
          teks:{
              type: String,
              default: ""
          },
          styleTitle:{
            type: String,
            default: ""
          }
      }
  }
  </script>
  
  <style>
    .underlineStyle{
        color:#00A3E1;
        border-bottom: 6px solid #DF1B22;
        text-align: center;
        font-weight: bold;
    }
    .commonStyle{
        color:white;
        text-align: center;
        font-weight: bold;
    }

    .backgndJudul{
        background: #DF1B22;
        border: 2px solid #DF1B22;
        border-top-left-radius: 20px;
        border-top-right-radius: 20px;
    }
  </style>