<template>
  <div>
    <input type="text" :placeholder="placeholder" v-model.trim="term" @keyup.enter="emitSearch"> 
    <button type="button" @click="emitSearch" >cerca</button>
  </div>
</template>

<script>
export default {
    name:'SearchBar',
    props:{
        placeholder: {
            type:String,
            required:false,
            default: 'cerca'

        },
        buttonText:{
            type:String,
            required:false,
            default:'cerca' 
        }
    },
    data(){
        return{
            term:'',
        }
    },
    methods:{
        emitSearch(){
            this.$emit('search',this.term);
        }
    }

}
</script>

<style>

</style>