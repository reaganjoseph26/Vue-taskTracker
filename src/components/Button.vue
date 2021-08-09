<template>
<!--@click === v-on: (both are two ways to add a method on a tag) -->
    <button @click="onClick()" :style="{background: color}" class="btn">{{text}}</button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        text:String,
        color: String,
    },
    methods: {
        onClick() {
            this.$emit('btn-click')
        }
    }
}
</script>
