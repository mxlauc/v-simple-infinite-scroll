<template>
    <v-simple-infinite-scroll @cargar="cargar" :distance="0" style="background-color:red">
        <ul>
            <li v-for="item in list" v-bind:key="item">{{item}}</li>
        </ul>
    </v-simple-infinite-scroll>
    
</template>
<script>
import VSimpleInfiniteScroll from '@/v-simple-infinite-scroll.vue';
export default {
    components: {
        VSimpleInfiniteScroll,
    },
    data(){
        return {
            list: []
        };
    },
    mounted(){
        
    },
    methods:{
        cargar(scroll){
            this.requestDataFromServer()
            .then(response=>{
                this.list = this.list.concat(response);
                if(this.list.length < 50){
                    scroll.loaded();
                }else{
                    scroll.complete();
                }
            });
            
        },
        async requestDataFromServer(){
            let arrayTemp = new Array();
            for(let i = 0; i < 5 ; i++){
                arrayTemp.push(Math.trunc(Math.random() * 1000));
            }
            await new Promise(resolve => setTimeout(resolve, 1000)); // 3 sec
            return arrayTemp;
        }
    }

}
</script>
<style scoped>

</style>