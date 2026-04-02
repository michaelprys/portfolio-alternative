<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <h1 class="title">Skills</h1>
            <h2 class="skills__subtitle">Tech Stack</h2>
            <ul class="skills__list" style="filter: grayscale(1)">
                <li>
                    <IconVue />
                    Vue 3
                </li>
                <li>
                    <IconQuasar />
                    Quasar
                </li>
                <li>
                    <IconTypeScript />
                    TypeScript
                </li>
                <li>
                    <IconPinia />
                    Pinia
                </li>
                <li>
                    <IconSupabase />
                    Supabase
                </li>
                <li>
                    <IconSass />
                    SASS
                </li>
                <li>
                    <IconTailwind />
                    Tailwind
                </li>
                <li style="filter: grayscale(1)">
                    <IconFigma />
                    Figma
                </li>
            </ul>
            <span class="book__page-number">3</span>

            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page2')">
                <IconBtnNext />
            </TurnButton>

            <TurnButton v-else @click="dropPage()">
                <IconBtnDrop />
            </TurnButton>
        </div>
    </div>
</template>

<script setup>
import TurnButton from '@/component/TurnButton.vue';
import IconAdobeXd from '@/component/icons/IconAdobeXd.vue';
import IconBtnDrop from '@/component/icons/IconBtnDrop.vue';
import IconBtnNext from '@/component/icons/IconBtnNext.vue';
import IconFigma from '@/component/icons/IconFigma.vue';
import IconPinia from '@/component/icons/IconPinia.vue';
import IconQuasar from '@/component/icons/IconQuasar.vue';
import IconSass from '@/component/icons/IconSass.vue';
import IconSupabase from '@/component/icons/IconSupabase.vue';
import IconTailwind from '@/component/icons/IconTailwind.vue';
import IconTypeScript from '@/component/icons/IconTypeScript.vue';
import IconVue from '@/component/icons/IconVue.vue';
import { useWindowSize } from '@vueuse/core';
import { inject } from 'vue';

const { width: windowWidth } = useWindowSize();
defineProps(['dropPage']);
const turnPage = inject('turnPage');

const handleTurnPage = (page) => {
    turnPage(page);
};
</script>

<style lang="scss">
.skills {
    &__subtitle {
        margin-top: $m-6;
        font-weight: bold;
        font-size: $fs-h6;
    }
    &__list {
        margin-top: $m-6;
        display: flex;
        flex-wrap: wrap;
        gap: $g-4;
        & li {
            display: flex;
            flex-direction: column;
            justify-content: center;
            gap: $g-2;
            align-items: center;
            max-width: 6.5rem;
            width: 100%;
            padding: 0.2em;
            border-radius: $br-8;
            box-shadow: $dc-shadow-inner;
            transition: box-shadow $tr-smooth;
            &:hover {
                box-shadow: 0 0 0.8rem rgba(0, 0, 0, 0.3);
            }
        }
    }
    &__icon {
        fill: rgb(117, 117, 117);
        width: 1.8rem;
        height: 1.8rem;
        &--pinia {
            fill: lighten(rgb(117, 117, 117), 14%);
        }
    }
}

@media (width <= $screen-sm) {
    .skills {
        &__subtitle {
            margin-top: $m-3;
            font-size: $fs-smaller;
        }
        &__list {
            margin-top: $m-4;
            & li {
                font-size: 0.7rem;
                width: 3.71rem;
            }
        }
    }
}

@media (width >= $screen-xs) and (width <= $screen-sm) {
    .skills {
        &__subtitle {
            margin-top: $m-6;
            font-size: $fs-smaller;
        }
        &__list {
            margin-top: $m-3_5;
            & li {
                font-size: 0.7rem;
                width: 3.5rem;
            }
        }
        &__icon {
            width: 1.4rem;
            height: 1.4rem;
        }
    }
}

@media (width <= $screen-xs) {
    .skills {
        &__subtitle {
            margin-top: $m-3;
        }
        &__list {
            margin-top: $m-3;
            & li {
                font-size: 0.6rem;
                width: 3rem;
                gap: $g-1;
            }
        }
        &__icon {
            width: 1rem;
            height: 1rem;
        }
    }
}
</style>
