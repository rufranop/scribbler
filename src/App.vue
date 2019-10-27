<template>
    <div class="app-container">
        <div class="note-holder">
            <textarea v-model="note" placeholder="Go on, write something amazing...️"></textarea>
        </div>
        <div class="about">
            <h1>scribbler.space <sup>beta</sup></h1>
            <p>A simple tool to store a note offline. Made with Vue.js.</p>
            <p>A project by <a href="https://twitter.com/paolorufrano" target="_blank">Paolo Rufrano</a></p>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                note: ''
            }
        },
        watch: {
            note(newNote) {
                localStorage.setItem('note', newNote);
            }
        },
        mounted() {
            if (localStorage) {
                this.note = localStorage.getItem('note');
            }
        }
    }
</script>

<style lang="scss">
    @import "./scss/styles.scss";
</style>
