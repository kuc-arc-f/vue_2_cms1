<template lang="html">
    <div>
        <h1>predict Input: </h1>
        <ul>
            <li>
                敷金 (n月分):
                <input type=text size=10 v-model="siki_price" value="0" /><br />
                <br />
            </li>
            <li>
                礼金(n月分):
                <input type=text size=10 v-model="rei_price" value="0" /><br />
                <br />
            </li>
            <li>
                面積:
                <input type=text size=10 v-model="menseki" value="0" /><br />
                <br />
            </li>
            <li>
                建築年数:
                <input type=text size=10 v-model="nensu" value="0" /><br />
                <br />
            </li>
            <li>
                駅 徒歩(分):
                <input type=text size=10 v-model="toho" value="0" /><br />
                <br />
            </li>
            <li>
                <button v-on:click="proc_check()">予測する</button>
            </li>
        </ul>

    </div>
</template>

<script>
import {Mixin} from '../../mixin'
import jQuery from 'jquery'

export default {
    mixins:[Mixin],
    created() {
        this.baseUrl = this.sysConst.API_BASE;
        console.log(this.sysConst.AJAX_MAX_TIME );
        console.log(this.baseUrl);
//        this.check_userState(this.sysConst.STORAGE_KEY_userData, this)
//        this.user_id = this.get_userId(this.sysConst.STORAGE_KEY_userData )
        /* console.log( 'new.uid ='+ this.user_id )  */
    },
    data() {
        return {
            siki_price: 0,
            rei_price: 0,
            menseki : 0,
            nensu : 0,
            toho : 0,
            user_id: '',
            baseUrl : '',
        }
    },
    methods: {
        proc_check: function() {
            var hostUrl= this.baseUrl + 'api_test';
            var siki_price = this.siki_price;
            var rei_price = this.rei_price;
            var menseki = this.menseki;
            var nensu = this.nensu;
            var toho = this.toho;
//            var content = this.content;
            console.log(hostUrl);
            jQuery.ajax({
                url: hostUrl,
                type:'POST',
                dataType: 'json',
                data : {
                     'siki_price' : siki_price ,
                     'rei_price' : rei_price ,
                     'menseki' : menseki,
                     'nensu' : nensu ,
                     'toho' : toho ,
                },
                timeout: this.sysConst.AJAX_MAX_TIME,
            }).done(function(data) {
                console.log("ajax-ok");
                console.log(data.price );
                alert(data.price )
            }).fail(function(XMLHttpRequest, textStatus, errorThrown) {
                console.log("ajax-error");
                console.log( errorThrown );
            })		
        },
    }
}
</script>
