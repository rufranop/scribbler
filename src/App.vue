<template>
    <div class="app-container" :class="{'dark-mode': darkMode}">
        <div class="note-holder">
            <textarea v-model="note" placeholder="Go on, write something amazing...️"></textarea>
        </div>
        <div class="about">
            <h1>scribbler.space <sup>beta</sup></h1>
            <p>A simple tool to store a note offline.</p>
            <p>Made with Vue.js.</p>
            <div class="tools">
                <button @click="toggleDark()">{{ darkMode ? 'Light Mode' : 'Dark Mode' }}</button>
                <div class="links">
                    <a href="https://github.com/rufranop/scribbler" target="_blank">
                        <svg><use xlink:href="#github"></use></svg>
                    </a>
                    <a href="https://twitter.com/paolorufrano" target="_blank">
                        <svg><use xlink:href="#twitter"></use></svg>
                    </a>
                </div>
            </div>
        </div>
        <icons />
    </div>
</template>

<script>
    import Icons from "./components/Icons";

    export default {
        name: 'app',
        components: {
            Icons
        },
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
