<template>
    <div class="app-container" :class="{'dark-mode': darkMode}">
        <div class="note-holder">
            <textarea v-model="note" placeholder="Go on, write something amazing...️"></textarea>
        </div>
        <div class="about">
            <h1>scribbler.space <sup>beta</sup></h1>
            <p>A simple tool to store a note offline. Made with Vue.js.</p>
            <p>A project by <a href="https://twitter.com/paolorufrano" target="_blank">Paolo Rufrano</a></p>
            <button @click="toggleDark()">{{ darkMode ? 'Light Mode' : 'Dark Mode' }}</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'app',
        data() {
            return {
                note: '',
                darkMode: false
            }
        },
        watch: {
            note(newNote) {
                localStorage.setItem('note', newNote);
            },
            darkMode() {
                localStorage.setItem('darkMode', this.darkMode)
            }
        },
        methods: {
            toggleDark() {
                this.darkMode = !this.darkMode;
            }
        },
        mounted() {
            if (localStorage) {
                this.note = localStorage.getItem('note');
                this.darkMode = JSON.parse(localStorage.getItem('darkMode'));
            }

            if (this.note === 'null' || this.note === null) {
                this.note = ''
            }

            // if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            //     this.darkMode = true;
            // }
        }
    }
</script>

<style lang="scss">
    @import "./scss/styles.scss";
</style>
