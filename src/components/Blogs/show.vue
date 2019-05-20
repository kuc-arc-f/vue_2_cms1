<template>
    <div>
        <h1>{{ item.title }}</h1>
        <br />
        <hr />
        <div v-html="item.content"></div>
    </div>
</template>

<script>
import axios from 'axios'
import marked from  'marked'
import {Mixin} from '../../mixin'

export default {
    mixins:[Mixin],
    created() {
        this.baseUrl = this.sysConst.API_BASE;
        console.log( this.baseUrl )        
    },
    data: function( ) {
        var itemDat = {title : '', content : ''}
        return {
            item: itemDat,
            editFlg: false,
            updated: false,
            baseUrl : '',
        }
    },
    mounted: function() {
        this.getItem()
    },
    methods: {
        getItem: function() {
            var url = this.baseUrl +'blogs/api_view/'+ this.$route.params.id;
            axios.get(url )
            .then( ( res ) => {
                this.item = res.data;
                this.item.content = marked(this.item.content)
                console.log(res.data )
            });            
        },
    }
}
</script>


