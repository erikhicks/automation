<template>
    <div class='all-tags'>
        <h2 class="ui dividing header">Filter by Tag</h2>
        <div class="ui six column grid">
            <div class="column">
                <p>Products</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['product'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
            <div class="column">
                <p>Systems</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['system'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
            <div class="column">
                <p>Displays</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['display'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
            <div class="column">
                <p>Components</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['component'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
            <div class="column">
                <p>Operating Systems</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['os'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
            <div class="column">
                <p>Peripherals</p>
                <div class='tag' v-bind:key="tag.name" v-for="tag in categories['peripheral'].tags" v-bind:class="{ 'selected': tag.selected, 'unselected': !tag.selected }" @click="toggleSelect(tag); $emit('filter-runners-by-tag', tags)">
                    <Tag v-bind:tag="tag" v-on:filter-runners-by-tag="$emit('filter-runners-by-tag', tags)" />
                </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import Tag from './Tag'

export default {
    name: 'AllTags',

    components: {
        Tag
    },

    props: [
        "tags"
    ],

    data() {
        return {
            categories: {}
        }
    },

    created() {
        this.tags.forEach(tag => {
            if (!this.categories[tag.category]) {
                this.categories[tag.category] = {
                    name: tag.categories,
                    tags: []
                }
            }

            this.categories[tag.category].tags.push(tag)
        });
    },

    methods: {
        toggleSelect(tag) {
            tag.selected = !tag.selected;
        }
    }
}
</script>

<style>
    .tag {
        cursor: pointer;
        margin-bottom: 5px;
    }
</style>

