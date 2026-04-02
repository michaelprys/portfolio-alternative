<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <div class="project project--lows-n-lines">
                <h2 class="title title--lows-n-lines">Featured project #2</h2>
                <a
                    class="project__link"
                    href="https://github.com/michaelprys/Lows-n-Lines"
                    target="_blank">
                    <div class="project__demo-wrapper">
                        <video class="project__video" loop muted plays-inline ref="video">
                            <source src="@img/content/lows-n-lines-demo.mp4" type="video/mp4" />
                        </video>
                        <picture>
                            <source srcset="@img/content/lows-n-lines.webp" type="image/webp" />
                            <img
                                @mouseover="playVideo"
                                @mouseleave="pauseVideo"
                                class="project__img"
                                src="@img/content/lows-n-lines.jpg"
                                alt="Lows n Lines app" />
                        </picture>
                    </div>
                </a>
                <div class="project__general-wrapper">
                    <div class="project__info">
                        <div class="project__wrapper">
                            <h2 class="project__name">Lows n Lines</h2>
                            <a
                                class="project__demo"
                                href="https://github.com/michaelprys/Lows-n-Lines"
                                target="_blank">
                                Code
                                <IconBtnDemo />
                            </a>
                        </div>
                        <span class="project__tech">
                            <span>Tech used:</span>
                            Nuxt, Shadcn, TailwindCSS, Valibot
                        </span>
                        <h3 class="project__description-heading">Description:</h3>
                        <p class="project__description">
                            Lows-n-Lines is a lowrider selling platform built with Nuxt and Shadcn,
                            currently in active development and expected to launch online soon. The
                            app already includes user authentication with customizable account
                            settings, allowing users to manage their profiles securely. Clients can
                            create inquiries by selecting from a variety of services. Additionally,
                            the platform offers a gallery view for browsing vehicles, providing a
                            visually engaging way to explore cars.
                        </p>
                    </div>
                    <div class="project__wrapper">
                        <span class="project__btn project__btn--soon">In development</span>
                    </div>
                </div>
            </div>
            <span class="book__page-number">5</span>

            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page3')">
                <IconBtnNext />
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
import IconBtnNext from '@/component/icons/IconBtnNext.vue';
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
    &__link {
        display: block;
        width: fit-content;
        margin-inline: auto;
    }
    &__demo-wrapper {
        position: relative;
        overflow: hidden;
        border-radius: $br-4;
        width: $w-64;
        height: 160.45px;
        box-sizing: border-box;
    }
    &__video {
        width: 100%;
        height: 100%;
        display: block;
        object-fit: cover;
        border: 8px solid rgba(83, 83, 83, 0.1);
        box-sizing: border-box;
        border-radius: $br-4;
        filter: grayscale(40%);
        transition: box-shadow $tr-smooth;
        box-shadow: 0 0 12.8px rgba(0, 0, 0, 0.3);
        &:hover {
            box-shadow: 0 0 16px rgba(0, 0, 0, 0.5);
        }
    }
    &__img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        box-sizing: border-box;
        border: 8px solid transparent;
        filter: grayscale(60%);
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
    &__btn {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: $m-7;
        color: $c-text;
        border-radius: $br-6;
        background-color: #e3e3e37b;
        width: $w-20;
        padding: $p-2;
        @include btn-big;

        &--soon {
            background-color: gray;
            width: $w-32;
            pointer-events: none;
            opacity: 0.7;
        }
    }
}

@media (width <= $screen-sm) {
    .project {
        &__demo-wrapper {
            width: 135px;
            height: 75.72px;
            margin-top: $m-4;
        }
        &__video,
        &__img {
            border-width: 8px;
        }
        &__info {
            margin-top: $m-3;
            gap: $g-1;
        }
        &__name {
            font-size: $fs-base;
        }
        &__tech,
        &__description-heading,
        &__description {
            font-size: 0.75rem;
            line-height: 1.4;
        }
        &__description {
            display: -webkit-box;
            -webkit-line-clamp: 6;
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-align: justify;
        }
        &__btn {
            margin-top: $m-4;
            padding-block: 0.25rem;
            font-size: $fs-small;

            &--soon {
                width: $w-32;
            }
        }
    }
}

@media (width <= $screen-xs) {
    .project {
        &__demo-wrapper {
            width: 135px;
            height: 75.72px;
        }
        &__description {
            -webkit-line-clamp: 4;
        }
        &__btn {
            margin-top: $m-2;
        }
    }
}
</style>
