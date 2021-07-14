# V Simple Infinite Scroll
A simple infinite scroll for your Vue3 projects.
## Installation
### NPM
```
npm install v-simple-infinite-scroll
```

### Direct include

You can use the CDN: https://unpkg.com/v-simple-infinite-scroll

```HTML
<script src="https://unpkg.com/v-simple-infinite-scroll@1.0.0/dist/v-simple-infinite-scroll.min.js"></script>
```


## Usage
Here is an example of your component that will contain your list.

The method appointed as the value of @cargar will be executed when the bottom of the element reaches the bottom of the viewport.


```HTML
<template>
    <v-simple-infinite-scroll
        @cargar="cargar"
        :distance="0"
        style="background-color:red">
        <ul>
            <li v-for="item in list" v-bind:key="item">
                {{item}}
            </li>
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
```

# Options

| Option | Description |
| ----- | ----- |
| load-to-fill | Boolean(default = true) - indicates if the infinite scroll must load items again until window is full. |
| distance | Number(default = 100) - Distance (px) between de bottom of the container and the bottom of the window. |

## Authors
[@mxlauc](https://github.com/mxlauc)
