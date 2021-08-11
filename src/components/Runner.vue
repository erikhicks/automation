<template>
    <div class='runner ui raised segment' v-bind:class="{ 'selected': runner.selected, 'unselected': !runner.selected }">
        <a class="ui green ribbon label">Online</a>
        <h4>{{ runner.displayName }} <small>({{ runner.id }})</small></h4>
        <div class="ui eight column grid">
            <!-- <div class="one wide column">Specs</div> -->
            <div class="sixteen wide column specs">
                <div class="ui horizontal list">
                    <div class="item" v-bind:key="runner.id + '-' + spec" v-for="spec in runner.specs">{{ spec }}</div>
                </div>
            </div>
        </div>
        <div class="ui eight column grid">
            <!-- <div class="one wide column">Tags</div> -->
            <div class="sixteen wide column">
                <div class="tag" v-bind:key="runner.id + '-' + tag.name" v-for="tag in runner.tags">
                    <Tag v-bind:tag="tag" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Tag from './Tag.vue'

export default {
    name: 'Runner',

    components: {
        Tag
    },
    
    props: [
        'runner'
    ],
}
</script>

<style scoped>
    .unselected {
        opacity: .5;
    }

    .tag {
        display: inline-block;
        margin: 5px;
    }

    .runner {
        margin-bottom: 20px !important;
    }
</style>