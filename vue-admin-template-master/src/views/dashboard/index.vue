<template>
  <div>
    <Card />
    <Sale />
    <Observe />
  </div>
</template>

<script>
import Card from './card'
import Sale from './sale'
import Observe from './observe'

export default {
  name:'',
  components:{
    Card,
    Sale,
    Observe
  },
  mounted(){
    this.$store.dispatch('getData')
  }
}
</script>

<style>

</style>