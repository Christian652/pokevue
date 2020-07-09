<template>
        <div class="card">
            <div class="card-image">
                <figure class="image" style="margin: 0px; display: flex; justify-content: center;">
                    <img :src="currentImg" alt="Apenas o Alt" style="width: 25%">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4">{{ name | upper }}</p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                    </div>
                </div>

                <div class="content">
                    <button class="button is-fullwidth is-primary" v-on:click="toggleImage($event)">{{ buttonValue }}</button>
                </div>
            </div>
        </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            pokemon: {
                type: '',
                front: '',
                back: ''
            },
            currentImg: '',
            buttonValue: 'Virar De Costas'
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    created() {
        axios.get(this.url).then(response => {
            this.pokemon.type = response.data.types[0].type.name
            this.pokemon.front = response.data.sprites.front_default
            this.pokemon.back = response.data.sprites.back_default
            this.currentImg = this.pokemon.front
        })

        console.log(this.pokemon)
    },
    filters: {
        upper(str) {
            var newName = str[0].toUpperCase() + str.slice(1);
            return newName
        }
    },
    methods: {
        toggleImage() {
            this.currentImg = this.currentImg == this.pokemon.front ? this.pokemon.back : this.pokemon.front
            this.buttonValue = this.buttonValue == "Virar De Costas" ? "Virar Para Frente" : "Virar De Costas" 
        }
    }
}
</script>

<style scoped>
    .card{
        margin-top: 1%;
    }
</style>