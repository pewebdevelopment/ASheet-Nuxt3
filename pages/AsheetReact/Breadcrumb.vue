<template>
    <div class="page-title-area tw-relative"
        :class="[showTitle ? 'tw-pt-15 tw-pb-10 md:tw-pt-20 md:tw-pb-15 lg:tw-pt-[100px] lg:tw-pb-20' : 'tw-pb-10 md:tw-pb-15 lg:tw-pb-20', props.class]">

        <div v-if="showTitle" class="tw-container">
            <h1 class="title tw-capitalize tw-mt-5 tw-mb-0 tw-text-3xl md:tw-text-4xl lg:tw-text-5xl tw-text-center">
                {{ title || currentPage}}
            </h1>
        </div>

        <h1 v-if="!showTitle" class="tw-sr-only">{{ title || currentPage}}</h1>
        <div class="page-breadcrumb tw-top-0 tw-left-0 tw-w-full" :class="[showTitle && 'tw-absolute']">
            <nav class="tw-container" aria-label="breadcrumbs">
                <ul class="breadcrumb tw-flex tw-flex-wrap tw-py-3">
                    <li :key="label" v-for="{ label, path } in pages"
                        class="tw-text-md first:before:tw-hidden before:tw-content-['/'] before:tw-mx-3.8 before:tw-color-body">
                        <Anchor :path="path"
                            className="tw-text-body cursor-pointer tw-capitalize tw-relative before:tw-absolute before:tw-content-[''] before:-tw-bottom-1.5 before:tw-right-0 before:tw-w-0 before:tw-h-px before:tw-transition-all before:tw-bg-heading hover:tw-text-heading hover:before:tw-left-0 hover:before:tw-w-full">
                            <span>{{ label }}1</span>
                        </Anchor>
                    </li>

                    <li class="tw-text-md tw-capitalize tw-text-heading first:before:tw-hidden before:tw-content-['/'] before:tw-mx-3.8 before:tw-color-body"
                        aria-current="page">
                        {{ currentPage }}
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</template>

<script setup lang="ts">
import Anchor from './Anchor.vue';

type TProps = {
    class?: string;
    pages: Array<{
        path: string;
        label: string;
    }>;
    currentPage: string;
    showTitle?: boolean;
    title?: string;
}

const props = withDefaults(defineProps<TProps>(), {
    showTitle: true,
})
</script>