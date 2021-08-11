<template>
    <div class='runners'>
        <h2 class="ui dividing header">Available Runners ({{ this.selectedRunners.length }})</h2>
        <div v-bind:key="runner.id" v-for="runner in selectedRunners">
            <Runner v-bind:runner="runner" />
        </div>
    </div>
</template>

<script>
import Runner from './Runner'

export default {
    name: 'Runners',

    components: {
        Runner
    },

    created() {
        //this.runners = runners
    },

    data() {
        return {
            runnerCount: 0,
        }
    },

    props: [
        "runners",
        "selectedRunners"
    ],

    watch: {
        selectedRunners: {
            handler: function(runners) {
                this.updateRunners(runners)
            }
        }
    },

    methods: {
        updateRunners(runners) {
            this.selectedRunners = runners
        }
    },
}
</script>

<style scoped>
    .runners {
        margin-top: 40px;
    }
</style>