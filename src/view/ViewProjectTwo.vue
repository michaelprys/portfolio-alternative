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
                                width="258px"
                                height="139px"
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
                        <span class="project__btn project__btn--soon">Coming soon</span>
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
.project__btn--soon {
    background-color: gray;
    width: $w-32;
    pointer-events: none;
}
</style>
