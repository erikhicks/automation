<template>
    <div :class="'ui label ' + (tag.selected? 'blue' : '')">
         <i :class="this.tagIconMap[tag.category] + ' icon'"></i>
        {{ tag.name }}
    </div>
</template>

<script>
export default {
    name: 'Tag',

    props: [
        "tag"
    ],

    data() {
        return {
            tagIconMap: {
                'product': 'window restore',
                'system': 'laptop',
                'component': 'microchip',
                'peripheral': 'usb',
                'os': 'hdd',
                'display': 'tv'
            }
        }
    },
}
</script>
