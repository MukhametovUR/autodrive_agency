<template>
    <div class="dialog" v-if="show" @clcik="hideDialog">
        <div class="content__dialog">
            <slot></slot>
        </div>
    </div>
</template>
<script>
export default {
    name:'MyDialog',
    props: {
        show: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideDialog() {
            this.$emit('update:show', false)
        }
    }
}
</script>
<style>
.dialog {
    top:0;
    left:0;
    right: 0;
    bottom: 0;
    background: rgba(0,0,0, 0.5);
    position: fixed;
}
.content__dialog {
    padding: 20px;
    background: #fff;
    border-radius: 10px;
    margin: auto;
}
</style>