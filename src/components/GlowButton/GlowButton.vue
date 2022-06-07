<template>
    <button class="glow-btn" :class="classes" :style="style">
        <template v-if="!label"><span><slot></slot></span></template>
        <template v-else><span>{{ label }}</span></template>
        <i></i>
    </button>
</template>
<script lang="ts" setup>
import { useAttrs, withDefaults } from 'vue'
import { GlowButtonVariants } from './types'

interface GlowButtonProps {
    variant?: string
    label?: string,
    dark?: boolean
}

const props = withDefaults(defineProps<GlowButtonProps>(), {
    variant: () => 'default',
    dark: false
})
const attrs = useAttrs()
const classes = [(attrs?.class || ''), props.dark ? 'dark' : '']

const style = {
    "--variant": (GlowButtonVariants as Record<string, string | undefined>)[props.variant] || props.variant 
}
</script>

<style lang="scss">
.glow-btn {
    position: relative;
    text-decoration: none;
    text-transform: uppercase;
    font-size: 1.2rem;
    letter-spacing: 0.1em;
    padding: 16px 30px;
    transition: 0.5s;
    background: #444;
    color: #fff;
    border: none;

    span {
        position: relative;
        z-index: 1;
    }

    i {
        position: absolute;
        inset: 0;
        display: block;

        &::before {
            content: '';
            position: absolute;
            top: -3.5px;
            left: 80%;
            width: 5px;
            height: 5px;
            border: 2px solid var(--variant);
            background: #27282c;
            transform: translateX(-50%);
            transition: 0.5s;
        }

        &::after {
            content: '';
            position: absolute;
            bottom: -3.5px;
            left: 20%;
            width: 5px;
            height: 5px;
            border: 2px solid var(--variant);
            background: #27282c;
            transform: translateX(-50%);
            transition: 0.5s;
        }
    }

    &:hover {
        letter-spacing: 0.25em;
        background: var(--variant);
        box-shadow: 0 0 35px var(--variant);
        color: var(--variant);

        i {
            &::before {
                width: 10px;
                left: 10%;
                box-shadow: 0 0 35px var(--variant);
            }   

            &::after {
                width: 10px;
                left: 90%;
                box-shadow: 0 0 35px var(--variant);
            } 
        }
    }

    &::before {
        content: '';
        position: absolute;
        inset: 2px;
        background: #27282c;
    }

    &.dark {
        background: #eee;
        color: #444;

        &::before {
            background: #ccc;
        }
    }


}

</style>