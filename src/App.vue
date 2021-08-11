<template lang="html">
    <div id="app" class="ui container">
        <AllTags v-bind:tags="tags" v-on:filter-runners-by-tag="filterRunners" ref="allTags" />
        <Runners v-bind:runners="runners" v-bind:selectedRunners="selectedRunners" />

        <button :class="'run ui compact labeled icon button ' + (validSelection ? 'green' : 'gray disabled')">
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
            this.selectedRunners = this.runners
            this.validSelection = this.runners.length > 0
        },

        data() {
            return {
                tags: [],
                unavailable_tags: [],
                selectedRunners: [],
                validSelection: false,
                runners: [
                    {
                        id: 'AT-WIN-INSP-1',
                        displayName: 'Dell Inspiron 3501',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'CinemaColor', selected: false, unavailable: false, category: 'product' },
                            { name: 'FHD', selected: false, unavailable: false, category: 'display' },
                            { name: 'Inspiron', selected: false, unavailable: false, category: 'system' },
                            { name: 'LCD', selected: false, unavailable: false, category: 'display' },
                            { name: 'Laptop', selected: false, unavailable: false, category: 'system' },
                            { name: 'Windows 10', selected: false, unavailable: false, category: 'os' },
                            { name: 'Intel', selected: false, unavailable: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, unavailable: false, category: 'component' },
                            { name: 'Intel Iris Xe', selected: false, unavailable: false, category: 'component' },
                            { name: '1920x1080 x 1.0', selected: false, unavailable: false, category: 'display', icon: 'cogs' },
                        ],
                        specs: [
                            'Windows 10 Pro (Build 19042)',
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
                        displayName: 'Dell Precision 3561',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'C6', selected: false, unavailable: false, category: 'peripheral' },
                            { name: 'Laptop', selected: false, unavailable: false, category: 'system' },
                            { name: 'Precision', selected: false, unavailable: false, category: 'system' },
                            { name: 'PremierColor', selected: false, unavailable: false, category: 'product' },
                            { name: 'Windows 10', selected: false, unavailable: false, category: 'os' },
                            { name: 'Intel', selected: false, unavailable: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, unavailable: false, category: 'component' },
                            { name: 'LCD', selected: false, unavailable: false, category: 'display' },
                            { name: 'UHD', selected: false, unavailable: false, category: 'display' },
                            { name: 'Intel UHD Graphics', selected: false, unavailable: false, category: 'component' },
                            { name: '1920x1080 x 1.0', selected: false, unavailable: false, category: 'display', icon: 'cogs' },
                        ],
                        specs: [
                            'Windows 10 Pro (Build 19042)',
                            'Memory: 22.9 GB / 32.00 GB',
                            'Storage: 500 GB',
                            'GPU: Intel UHD Graphics',
                            'Video Driver Version: 27.20.100.9664',
                            'Video Resolution: 3840 x 2160 x 60 hertz',
                            'Video Bits/Pixel: 32'
                        ]
                    },
                    {
                        id: 'AT-WIN-SPEC-1',
                        displayName: 'HP Spectre x360 Convertible',
                        selected: true,
                        status: 'running',
                        tags: [
                            { name: 'Laptop', selected: false, unavailable: false, category: 'system' },
                            { name: 'Spectre', selected: false, unavailable: false, category: 'system' },
                            { name: 'DisplayControl', selected: false, unavailable: false, category: 'product' },
                            { name: 'Windows 10', selected: false, unavailable: false, category: 'os' },
                            { name: 'Intel', selected: false, unavailable: false, category: 'component' },
                            { name: 'Rocket Lake', selected: false, unavailable: false, category: 'component' },
                            { name: 'LCD', selected: false, unavailable: false, category: 'display' },
                            { name: 'FHD', selected: false, unavailable: false, category: 'display' },
                            { name: 'Intel Iris Xe', selected: false, unavailable: false, category: 'component' },
                            { name: '1920x1080 x 1.0', selected: false, unavailable: false, category: 'display', icon: 'cogs' },
                        ],
                        specs: [
                            'Windows 10 Pro (Build 19042)',
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

                this.tags.sort((a,b) => (a.name > b.name) ? 1 : -1)
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
                })

                this.unavailable_tags = []
                let remainingAvailableTags = []

                this.tags.forEach(tag => {
                    this.selectedRunners.forEach(runner => {
                        runner.tags.forEach(runnerTag => {
                            if (tag.name === runnerTag.name) {
                                remainingAvailableTags.push(runnerTag)
                            }
                        })
                    })
                })

                this.tags.forEach(tag => {
                    if (!remainingAvailableTags.some(t => t.name === tag.name)) {
                        this.unavailable_tags.push(tag)
                    }
                })

                this.$refs.allTags.disable(this.unavailable_tags)
                this.validSelection = (this.selectedRunners.length > 0)
            }
        }
    }
</script>

<style>
    #app {
        margin-top: 20px;
    }

    .run.disabled {
        visibility: hidden;
    }
</style>