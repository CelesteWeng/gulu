<template>
    <button class="g-button celeste2" :class="{ [`icon-${iconPosition}`]: true }" @click="$emit('click')">
        <g-icon v-if="icon && !loading" class="icon" :name="icon"></g-icon>
        <g-icon v-if="loading" class="icon loading" name="loading"></g-icon>
        <div class="content">
            <slot/>
        </div>
    </button>
</template>
<script>
    import Vue from 'vue'
    import Icon from './icon'
    Vue.component('g-icon', Icon)

    export default {
        name: "GuluButton",
        component: {
            'g-icon': Icon
        },
        props: {
            icon: {},
            loading: {
                type: Boolean,
                default: false
            },
            iconPosition: {
                type: String,
                default: "left",
                validator(value) {
                    return value === "left" || value === "right"
                }
            }
        }
    }
</script>
<style lang="scss" scoped>
    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
    }
    .g-button {
        display: inline-flex; justify-content: center;
        align-items: center; vertical-align: middle;
        font-size: var(--font-size); height: var(--button-height);
        padding: 0 1em; border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        &:hover { border-color: var(--border-color-hover); }
        &:active { background-color: var(--button-active-bg); }
        &:focus { outline: none; }
        > .icon { order: 1; margin-right: .1em; }
        > .content { order: 2; }

        &.icon-right {
            > .icon { order: 2; margin-left: .1em; }
            > .content { order: 1; }
        }
    }
    .loading {
        animation: 2s spin infinite linear;
    }
</style>