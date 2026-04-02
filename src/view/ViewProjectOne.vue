<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <h1 class="title">Featured project #1</h1>
            <div class="project">
                <a
                    class="project__link"
                    href="https://zigzags-workshop.netlify.app"
                    target="_blank">
                    <div class="project__demo-wrapper">
                        <video class="project__video" loop muted plays-inline ref="video">
                            <source src="@img/content/zigzags-workshop-demo.mp4" type="video/mp4" />
                        </video>
                        <picture>
                            <source srcset="@img/content/zigzags-workshop.webp" type="image/webp" />
                            <img
                                @mouseover="playVideo"
                                @mouseleave="pauseVideo"
                                class="project__img"
                                src="@img/content/zigzags-workshop.jpg"
                                width="256px"
                                height="136px"
                                alt="zigzags-workshop app" />
                        </picture>
                    </div>
                </a>
                <div class="project__general-wrapper">
                    <div class="project__info">
                        <div class="project__wrapper">
                            <h2 class="project__name">Zigzag's Workshop</h2>
                            <a
                                class="project__demo"
                                href="https://github.com/michaelprys/ZigZags_Workshop"
                                target="_blank">
                                Code
                                <IconBtnDemo />
                            </a>
                        </div>
                        <span class="project__tech">
                            <span>Tech used:</span>
                            Vue 3, Quasar, Supabase, Stripe, TypeScript, Sass, Pinia
                        </span>
                        <h3 class="project__description-heading">Description:</h3>
                        <p class="project__description">
                            A gamified e-commerce app built with Vue 3 and Quasar, offering a
                            responsive and intuitive interface. Features Stripe integration for
                            topping up virtual balance and making purchases in the user's preferred
                            currency. The backend is handled with Supabase, using edge functions and
                            a custom PostgreSQL database. State management is implemented with
                            Pinia, and an inventory system allows users to manage their purchased
                            items.
                        </p>
                    </div>
                    <a
                        class="project__btn"
                        href="https://zigzags-workshop.netlify.app"
                        target="_blank">
                        Project
                    </a>
                </div>
            </div>
            <span class="book__page-number">4</span>

            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page2')">
                <IconBtnPrev />
            </TurnButton>

            <TurnButton v-else @click="dropPage">
                <IconBtnDrop />
            </TurnButton>
        </div>
    </div>
</template>

<script setup>
import TurnButton from '@/component/TurnButton.vue';
import IconBtnDemo from '@/component/icons/IconBtnDemo.vue';
import IconBtnDrop from '@/component/icons/IconBtnDrop.vue';
import IconBtnPrev from '@/component/icons/IconBtnPrev.vue';
import { usePlayVideo } from '@/use/usePlayVideo';
import { useWindowSize } from '@vueuse/core';
import { inject } from 'vue';
const { video, playVideo, pauseVideo } = usePlayVideo();

const { width: windowWidth } = useWindowSize();

defineProps(['dropPage']);
const turnPage = inject('turnPage');

const handleTurnPage = (page) => {
    turnPage(page);
};
</script>

<style lang="scss">
.project {
    &__wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    &__video {
        margin-top: $m-6;
        border-radius: $br-4;
        width: $w-64;
        margin-inline: auto;
        border: 8px solid rgba($c-text, 10%);
        transition: box-shadow $tr-smooth;
        box-shadow: 0 0 12.8px rgba(0, 0, 0, 0.3);
        filter: grayscale(40%);
        &:hover {
            box-shadow: 0 0 16px rgba(0, 0, 0, 0.5);
        }
    }
    &__link {
        margin-inline: auto;
    }
    &__demo-wrapper {
        position: relative;
    }
    &__img {
        position: absolute;
        filter: grayscale(60%);
        border: 8px solid rgba($c-text, 0%);
        top: 50%;
        left: 50%;
        object-fit: cover;
        transform: translateY(-50%) translateX(-50%);
        transition: opacity $tr-smooth;
        &:hover {
            opacity: 0;
        }
    }
    &__name {
        font-size: $fs-h4;
    }
    &__info {
        margin-top: $m-5;
        display: flex;
        flex-direction: column;
        gap: $g-2;
    }
    &__tech {
        margin-top: $m-2;
    }
    &__tech span,
    &__description-heading {
        font-weight: bold;
    }
    &__tech,
    &__description-heading,
    &__description {
        font-size: $fs-medium;
    }
    &__demo {
        position: relative;
        display: flex;
        align-items: center;
        gap: $g-2;
        color: $c-text;
        transition: fill $tr-basic;
        & svg {
            fill: $c-text;
        }
        &::after {
            position: absolute;
            content: '';
            width: 100%;
            height: 0.125rem;
            background-color: rgba($c-text, 65%);
            bottom: -0.125rem;
            transform: scaleX(0);
            transition: transform $tr-fast;
            transform-origin: left;
        }
        &:hover::after {
            transform: scale(1);
        }
    }
    &__btn,
    &__more-projects-btn {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: $m-7;
        color: $c-text;
        border-radius: $br-6;
        background-color: #e3e3e37b;
        @include btn-big;
    }
    &__btn {
        width: $w-20;
    }
    &__more-projects-btn {
        width: 8.5rem;
    }
    &__btn,
    &__more-projects-btn {
        padding: $p-2;
    }
}

@media (width <= $screen-sm) {
    .project {
        &__demo-wrapper {
            padding-inline: 4rem;
        }
        &__video {
            margin-top: $m-5;
        }
        &__img {
            height: 100%;
        }
        &__name {
            font-size: $fs-h6;
        }
        &__info {
            font-size: 0.875rem;
        }
        &__tech,
        &__description-heading,
        &__description {
            font-size: 0.875rem;
        }
        &__code-btn,
        &__more-projects-btn {
            font-size: $fs-smaller;
            padding-block: 0.125rem;
            margin-top: $m-3_5;
        }
    }
}

@media (width >= $screen-xs) and (width <= $screen-sm) {
    .project {
        &__name {
            font-size: $fs-base;
        }
        &__tech,
        &__description-heading,
        &__description {
            font-size: 0.75rem;
            text-align: justify;
        }
        &__code-btn,
        &__more-projects-btn {
            padding-block: 0.1rem;
            margin-top: $m-3_5;
        }
    }
}
@media (width <= $screen-xs) {
    .project {
        &__name {
            font-size: $fs-small;
        }
        &__info {
            font-size: 0.8rem;
        }
        &__demo-icon {
            width: 1.2rem;
            height: 1.2rem;
        }
        &__tech,
        &__description-heading,
        &__description {
            font-size: 0.7rem;
            text-align: justify;
            margin-top: 0;
            line-height: 1.6;
        }
        &__code-btn,
        &__more-projects-btn {
            width: 6rem;
            padding-block: 0;
            font-size: 0.65rem;
            margin-top: $m-3_5;
        }
    }
}
</style>
