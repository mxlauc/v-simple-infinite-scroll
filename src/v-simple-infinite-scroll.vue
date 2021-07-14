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
            cargando : false,
            completed : false
        }
    },
    props: {
        distance : {
            type: Number,
            default: 100
        },
        loadToFill : {
            type: Boolean,
            default: true
        }
    },
    emits: [
        'cargar'
    ],
    mounted(){
        this.aplicarListener();
        this.handleScroll();
    },
    unmounted(){
        this.desvincularListener();
    }
    ,
    watch: {

    },
    methods: {
        handleScroll(){
			if (!this.cargando && this.$refs.contenedor.getBoundingClientRect().bottom < (window.innerHeight + this.distance)) {
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
            this.cargando = true;
            this.$emit('cargar', this);
        },
        loaded(){
            //waiting 300 ms for items to be rendered
            setTimeout(()=>{
                this.cargando = false;
                this.tryToFill();
            }, 300);
        },
        complete(){
            this.cargando = false;
            this.completed = true;
            this.desvincularListener();
        },
        tryToFill(){
            this.handleScroll();
        }
    }
}
</script>
<style scoped>

</style>
