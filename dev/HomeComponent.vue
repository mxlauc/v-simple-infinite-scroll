<template>
    <div class="container">
        <v-simple-infinite-scroll @cargar="cargar" :distance="0">
            <div class="row masonry-row">
                <div class="grid-item col col-12 col-md-6 col-lg-4 col-xl-3 mb-3" v-for="(item, index) in list" v-bind:key="item">
                    <div class="square" :style="{height: item + 'px'}">
                        <h3 style="margin-top: 0px;">{{index + 1}} Item</h3>    
                        <span>Height {{item}}px</span>
                    </div>
                </div>
                <div class="grid-item col col-12 col-md-6 col-lg-4 col-xl-3 mb-3" id="v-simple-infinite-scroll-bottom">
                </div>
            </div>
            
        </v-simple-infinite-scroll>
    </div>
</template>


<script>
import VSimpleInfiniteScroll from '@/v-simple-infinite-scroll.vue';
import Masonry from 'masonry-layout';
import 'bootstrap/dist/css/bootstrap.min.css';
import 'bootstrap/dist/js/bootstrap.js';

export default {
    components: {
        VSimpleInfiniteScroll,
    },
    data(){
        return {
            list: [],
        };
    },
    mounted(){
        
    },
    methods:{
        cargar(scroll){
            this.requestDataFromServer()
            .then(response=>{
                this.list = this.list.concat(response);
                if(this.list.length < 300){
                    setTimeout(()=>{
                        this.aplicarMasonry();
                    },0);
                    
                    scroll.loaded();
                }else{
                    scroll.complete();
                }
            });
            
        },
        async requestDataFromServer(){
            let arrayTemp = new Array();
            for(let i = 0; i < 3 ; i++){
                arrayTemp.push(Math.trunc(Math.random() * 5) * 60 + 100);
            }
            await new Promise(resolve => setTimeout(resolve, 1000)); // 3 sec
            return arrayTemp;
        },
        aplicarMasonry(){
            new Masonry( '.masonry-row', {
                
            });
        }
    }

}
</script>
<style scoped>
    *{
        font-family: sans-serif;
    }
    .square{
        text-align: center;
        background-color: #ccc;
        width: 100%;
        border-radius: 5px;
        align-items: center;   /* <---- NEW    */
        display: flex;
        justify-content: center;
    }
</style>