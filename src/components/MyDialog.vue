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
        display: flex;
        justify-content: center;

    top:0;
    left:0;
    right: 0;
    bottom: 0;
    background: rgba(0,0,0, 0.5);
    position: fixed;
    margin: auto;

}
.content__dialog {
    padding: 24px;
    background: #fff;
    border-radius: 10px;
    margin: auto;
    max-width:1000px;

}
</style>