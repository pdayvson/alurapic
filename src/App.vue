<template>
    <div class="corpo">
        <h1 class="centralizada">{{ titulo }}</h1>
        <ul class="lista-fotos">
            <li class="lista-fotos-item" v-for="foto in fotos">
                <meu-painel :titulo="foto.titulo">
                    <img class="imagem-responsiva" :src="foto.url" :alt="foto.titulo">
                </meu-painel>
            </li>
        </ul>
    </div>
</template>

<script>
    import Paniel from './components/shared/paniel/Painel.vue'

    export default {
        components: {
            'meu-painel': Paniel
        },
        data () {
            return {
                titulo: "Alurapic",
                fotos: []
            }
        },
        created() {
            this.$http.get("http://localhost:3000/v1/fotos")
                .then(res => res.json())
                .then(fotos => this.fotos = fotos);
        }
    }
</script>

<style>
    .corpo {
        font-family: Helvetica, sans-serif;
        width: 96%;
        margin: 0 auto;
    }

    .centralizada {
        text-align: center;
    }

    .lista-fotos {
        list-style: none;
    }

    .lista-fotos-item {
        display: inline-block;
    }

    .imagem-responsiva {
        width: 100%;
    }
</style>