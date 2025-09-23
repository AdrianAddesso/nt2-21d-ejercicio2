<template>
    <div class="container-fluid mt-3" id="app">
        <main>
            <Buscador/>
            <img style ="margin-top: 200px;" src="https://content.imageresizer.com/images/memes/cheems-meme-3nzkub.png" width="100px"></img>
        </main>
    </div>
</template>

<script setup>
    import Buscador from './components/Buscador.vue'
</script>

<style>
html, body, #app  {
    background-color: rgb(239, 228, 228);
}
</style>
