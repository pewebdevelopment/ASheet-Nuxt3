<template>
    <template v-if="path">
        <template v-if="!internal">
            <a v-if="isHash" :class="className" :rel="rel" :href="path" @click="onClick" @focus="onFocus" @blur="onBlur">
                <slot></slot>
            </a>
            <a v-else :class="className" :rel="rel" :target="target" :href="path" @click="onClick" @focus="onFocus"
                @blur="onBlur">
                <slot></slot>
            </a>
        </template>
        <NuxtLink v-else :href="path" :to="path">
            <a :class="className" @click="onClick">
                <slot></slot>
            </a>
        </NuxtLink>
    </template>
</template>

<script setup lang="ts">
import { defineProps, computed, AnchorHTMLAttributes } from 'vue';
// import { TProps } from './AnchorTypes'
interface AnchorNamedAttrs {
    path: string;
    className?: string;
    onClick?: (e: MouseEvent) => void;
    onKeyPress?: (e: KeyboardEvent) => void;
    onFocus?: (e: FocusEvent) => void;
    onBlur?: (e: FocusEvent) => void;
}

interface TProps extends AnchorHTMLAttributes, AnchorNamedAttrs {
    target?: string,
    rel?: string,
}

const props = withDefaults(defineProps<TProps>(), {
    target: "_blank",
    rel: "noopener noreferrer",
})

const internal = computed(() => {
    return /^\/(?!\/)/.test(props.path)
})

const isHash = computed(() => {
    return props.path.startsWith('#')
})
</script>