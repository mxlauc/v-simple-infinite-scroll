<template>
asdfas
<br><br><br><br><br>
    <div class="container">
        <div v-if="true" class="v-simple-infinite-scroll-container shadow-lg" style="border:0px solid black; height: 500px; overflow-y:scroll;">
            <v-simple-infinite-scroll @load="cargar" :distance="0">
                <div class="grid-item m-3" v-for="(item, index) in list" v-bind:key="item">
                    <div class="square" :style="{height: item + 'px'}">
                        <h3 style="margin-top: 0px;">{{index + 1}} Item</h3>    
                        <span>Height {{item}}px</span>
                    </div>
                </div>
            </v-simple-infinite-scroll>
        </div>

        <v-simple-infinite-scroll @load="cargar" :distance="0" v-if="false">
            <div class="row masonry-row">
                <div class="grid-item col col-12 col-md-6 col-lg-4 col-xl-3 mb-3" v-for="(item, index) in list" v-bind:key="item">
                    <div class="square" :style="{height: item + 'px'}">
                        <h3 style="margin-top: 0px;">{{index + 1}} Item</h3>    
                        <span>Height {{item}}px</span>
                    </div>
                </div>
                <div class="grid-item col col-12 col-md-6 col-lg-4 col-xl-3 mb-3 v-simple-infinite-scroll-bottom">
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
                if(this.list.length < 20){
                    scroll.loaded();
                }else{
                    scroll.complete();
                }
                setTimeout(()=>{
                    //this.aplicarMasonry();
                },10);
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