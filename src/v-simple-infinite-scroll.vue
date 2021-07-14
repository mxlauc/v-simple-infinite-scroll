<template>
    <div ref="contenedor">
        <slot></slot>
        <slot name="cargando" v-if="cargando"></slot>

    </div>
</template>
<script>
export default {
    data(){
        return {
            cargando : false
        }
    },
    props: {
        distance : {
            type: Number,
            default: 100
        }
    },
    emits: [
        'cargar'
    ],
    mounted(){
        console.log("hola scroll");
        this.aplicarListener();
    },
    unmounted(){
        this.desvincularListener();
    }
    ,
    watch: {

    },
    methods: {
        handleScroll(){
			if ( this.$refs.contenedor.getBoundingClientRect().bottom < (window.innerHeight + this.distance)) {
				this.loadMorePosts();
			}
        },
        aplicarListener(){
            window.addEventListener("scroll", this.handleScroll)
        },
        desvincularListener(){
			window.removeEventListener("scroll", this.handleScroll)
        },
        loadMorePosts(){
            if(!this.cargando){
                this.cargando = true;
                console.log("emitiendo...");
                this.$emit('cargar', this);

            }

        },
        loaded(){
            setTimeout(()=>{
                this.cargando = false;
                console.log("cargo!");
            }, 300);
        },
        complete(){
            console.log("ya no hya mas");
        }
    }
}
</script>
<style scoped>

</style>
