<template>
  <div id="app">

    <v-table
    :users_data="USERS"
    />
  </div>
</template>


<script>
import {mapActions, mapGetters} from  'vuex'
import  vTable from './components/table/v-table'
export default {
    name:'app',
    components: {
        vTable
    },
    computed:{
        ...mapGetters([
            'USERS'
        ])
    },

    methods:{
        ...mapActions([
            'GET_USERS_FROM_API'
        ])
    },
  mounted(){
    this.GET_USERS_FROM_API()
  },
}

</script>
