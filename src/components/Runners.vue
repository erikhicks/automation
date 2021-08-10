<template>
    <div class='runners'>
        <h2 class="ui dividing header">Available Runners ({{ this.selectedRunners }})</h2>
        <div v-bind:key="runner.id" v-for="runner in runners">
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

    data() {
        return {
            runnerCount: 0
        }
    },

    mounted() {
        this.runnerCount = this.runners.length
    },

    updated() {
        this.runnerCount = this.runners.filter(runner => {
            return runner.selected
        }).length
    },

    props: [
        "runners",
        "selectedRunners"
    ],
}
</script>

<style scoped>
    .runners {
        margin-top: 40px;
    }
</style>