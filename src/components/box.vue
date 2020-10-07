<template>
    <div class="columns">
        <div class="column" v-show="se">
           <input v-model="Fecha" type="number">
           <input v-model="edad" type="number">
            <p v-show="se">{{ años }}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'box',
  data () {
    return {
        edad: '',
        Fecha: 2018,
        se: false
   }
 },
  computed: {
      años () {
          return this.Fecha - this.edad
      }
  },
  watch: {
      edad (keydown) {
          this.se = true
          console.log('algo cambio')
      }
  }
}
</script>

<style scoped="true" lang="scss">
    .box{
        background: rgba(255,83,92,1);
background: -moz-linear-gradient(left, rgba(255,83,92,1) 0%, rgba(253,115,108,1) 100%);
background: -webkit-gradient(left top, right top, color-stop(0%, rgba(255,83,92,1)), color-stop(100%, rgba(253,115,108,1)));
background: -webkit-linear-gradient(left, rgba(255,83,92,1) 0%, rgba(253,115,108,1) 100%);
background: -o-linear-gradient(left, rgba(255,83,92,1) 0%, rgba(253,115,108,1) 100%);
background: -ms-linear-gradient(left, rgba(255,83,92,1) 0%, rgba(253,115,108,1) 100%);
background: linear-gradient(to right, rgba(255,83,92,1) 0%, rgba(253,115,108,1) 100%);
filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#ff535c', endColorstr='#fd736c', GradientType=1 );
    }
@media(max-width: 600px){
     .box
    {
        margin-right: 85%;
    }
}
@media(min-width: 599px){
  .box
    {
    margin-right: 80%;
    }
}
</style>
