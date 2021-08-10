<template lang="html">
    <div id="app" class="ui container">
        <AllTags v-bind:tags="tags" v-on:filter-runners-by-tag="filterRunners" />
        <Runners v-bind:runners="runners" v-bind:selectedRunners="selectedRunners" />

        <button :class="'ui compact labeled icon button ' + (validSelection ? 'green' : 'gray disabled')">
            <i class="play icon"></i>
            Run Automation
        </button>
    </div>
</template>

<script>
    import AllTags from './components/AllTags'
    import Runners from './components/Runners'

    export default {
        name: 'app',
        components: {
            AllTags,
            Runners,
        },

        created() {
            this.getAllTags()
            this.selectedRunners = this.runners.length
            this.validSelection = this.runners.length > 0
        },

        data() {
            return {
                tags: [],
                selectedRunners: 0,
                validSelection: false,
                runners: [
                    {
                        id: 'AT-WIN-INSP-1',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'CinemaColor', selected: false, category: 'product' },
                            { name: 'FHD', selected: false, category: 'display' },
                            { name: 'Inspiron', selected: false, category: 'system' },
                            { name: 'LCD', selected: false, category: 'display' },
                            { name: 'Laptop', selected: false, category: 'system' },
                            { name: 'Windows 10', selected: false, category: 'os' },
                            { name: 'Intel', selected: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, category: 'component' },
                        ],
                        specs: [
                            'Dell Inspiron 3501',
                            'OS: Windows 10 Pro (Build 19042)',
                            'Memory: 3.33 GB / 8.00 GB',
                            'Storage: 250 GB',
                            'GPU: Intel Iris Xe',
                            'Video Driver Version: 27.20.100.9365',
                            'Video Resolution: 1920 x 1080 x 59 hertz',
                            'Video Bits/Pixel: 32'
                        ]
                    },
                    {
                        id: 'AT-WIN-PREC-2',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'C6', selected: false, category: 'peripheral' },
                            { name: 'Laptop', selected: false, category: 'system' },
                            { name: 'Precision', selected: false, category: 'system' },
                            { name: 'PremierColor', selected: false, category: 'product' },
                            { name: 'Windows 10', selected: false, category: 'os' },
                            { name: 'Intel', selected: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, category: 'component' },
                            { name: 'LCD', selected: false, category: 'display' },
                            { name: 'UHD', selected: false, category: 'display' }
                        ],
                        specs: [
                            'Dell Precision 3561',
                            'OS: Windows 10 Pro (Build 19042)',
                            'Memory: 22.9 GB / 32.00 GB',
                            'Storage: 500 GB',
                            'GPU: Intel UHC Graphics',
                            'Video Driver Version: 27.20.100.9664',
                            'Video Resolution: 3840 x 2160 x 60 hertz',
                            'Video Bits/Pixel: 32'
                        ]
                    },
                    {
                        id: 'AT-WIN-SPEC-1',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'Laptop', selected: false, category: 'system' },
                            { name: 'Spectre', selected: false, category: 'system' },
                            { name: 'DisplayControl', selected: false, category: 'product' },
                            { name: 'Windows 10', selected: false, category: 'os' },
                            { name: 'Intel', selected: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, category: 'component' },
                            { name: 'LCD', selected: false, category: 'display' },
                            { name: 'FHD', selected: false, category: 'display' }
                        ],
                        specs: [
                            'HP Spectre x360 Convertible',
                            'OS: Windows 10 Pro (Build 19042)',
                            'Memory: 3.84 GB / 8.00 GB',
                            'Storage: 1 TB',
                            'GPU: Intel Iris Xe',
                            'Video Driver Version: 27.20.100.9079',
                            'Video Resolution: 1920 x 1080 x 60 hertz',
                            'Video Bits/Pixel: 32'
                        ]
                    }
                ],
            }
        },

        methods: {
            getAllTags() {
                this.runners.forEach(runner => {
                    runner.tags.forEach(tag => {
                        if (!this.tags.some(t => t.name === tag.name)) {
                            this.tags.push(tag)
                        }
                    })
                })
            },

            filterRunners(tags) {
                let selectedTags = tags.filter(tag => tag.selected === true)
                
                this.runners.forEach(runner => {
                    runner.selected = true
                    selectedTags.forEach(selectedTag => {
                       if (!runner.tags.some(t => t.name === selectedTag.name)) {
                           runner.selected = false
                       }
                    })

                   runner.tags.forEach(runnerTag => {
                        if (selectedTags.some(t => t.name === runnerTag.name)) {
                           runnerTag.selected = true
                        } else {
                            runnerTag.selected = false
                        }
                    })
                })

                this.selectedRunners = this.runners.filter(runner => {
                    return runner.selected == true
                }).length

                this.validSelection = this.selectedRunners > 0
            }
        }
    }
</script>

<style>
    #app {
        margin-top: 20px;
    }
</style>