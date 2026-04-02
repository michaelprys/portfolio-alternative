<template>
    <div class="background-image"></div>
    <BackgroundOverlay />
    <div class="container">
        <div
            class="tablet"
            :class="{
                'fade-in': isFadeInDone,
                'show-tablet': isShowTabletDone,
            }">
            <div class="tablet__clamp"></div>
            <div class="tablet__page">
                <div class="tablet__overlay"></div>
            </div>
            <div class="tablet__page" ref="page7Ref">
                <ViewContact :toIntroPage="() => toIntroPage()" />
            </div>
            <div class="tablet__page" ref="page6Ref">
                <ViewMoreAboutMe :dropPage="() => dropPage('page6')" />
            </div>
            <div class="tablet__page" ref="page5Ref">
                <ViewProjectTwo :dropPage="() => dropPage('page5')" />
            </div>
            <div class="tablet__page" ref="page4Ref">
                <ViewProjectOne :dropPage="() => dropPage('page4')" />
            </div>
            <div class="tablet__page" ref="page3Ref">
                <ViewSkills :dropPage="() => dropPage('page3')" />
            </div>
            <div class="tablet__page" ref="page2Ref">
                <ViewServices :dropPage="() => dropPage('page2')" />
            </div>
            <div class="tablet__page" ref="page1Ref">
                <ViewAbout :dropPage="() => dropPage('page1')" />
            </div>
            <div class="tablet__page" ref="page0Ref">
                <ViewIntro :dropPage="() => dropPage('page0')" :toLastPage="toLastPage" />
            </div>
        </div>
    </div>
</template>

<script setup>
import ViewIntro from '@/view/ViewIntro.vue';
import ViewAbout from '@/view/ViewAbout.vue';
import ViewServices from '@/view/ViewServices.vue';
import ViewSkills from '@/view/ViewSkills.vue';
import ViewProjectOne from '@/view/ViewProjectOne.vue';
import ViewProjectTwo from '@/view/ViewProjectTwo.vue';
import ViewMoreAboutMe from '@/view/ViewMoreAboutMe.vue';
import ViewContact from '@/view/ViewContact.vue';
import BackgroundOverlay from '@/component/BackgroundOverlay.vue';
import { ref, provide, onMounted, watchEffect } from 'vue';
import SfxTurn from '@/assets/sounds/page-turn.wav?url';
import Sfx6 from '@/assets/sounds/page-shuffle.mp3?url';
import { usePlaySfx } from '@/use/usePlaySfx';
import { useWindowSize } from '@vueuse/core';

const { width: windowWidth } = useWindowSize();
const { playSfx } = usePlaySfx();

const pageStates = ref({
    page0: false,
    page1: false,
    page2: false,
    page3: false,
    page4: false,
    page5: false,
    page6: false,
    page7: false,
});

const page0Ref = ref(null);
const page1Ref = ref(null);
const page2Ref = ref(null);
const page3Ref = ref(null);
const page4Ref = ref(null);
const page5Ref = ref(null);
const page6Ref = ref(null);
const page7Ref = ref(null);

const pageRefs = [page0Ref, page1Ref, page2Ref, page3Ref, page4Ref, page5Ref, page6Ref, page7Ref];
const pages = Object.keys(pageStates.value);
const isAnimationInProgress = ref(false);

const randomizePageFall = () => {
    return `rotateZ(${Math.floor(Math.random() * (3 - -7) + -7)}deg) translateY(150%)`;
};

const dropPage = (page) => {
    if (!isAnimationInProgress.value) {
        pageStates.value[page] = !pageStates.value[page];
        const index = pages.indexOf(page);
        if (pageRefs[index] && pageRefs[index].value) {
            pageRefs[index].value.style.transform = randomizePageFall();
            playSfx(SfxTurn);
        }
    }
};

provide('turnPage', (page) => dropPage(page));
provide('isAnimationInProgress', isAnimationInProgress);

const toLastPage = () => {
    if (!isAnimationInProgress.value) {
        isAnimationInProgress.value = true;
        pages.slice(0, 7).forEach((page, index) => {
            setTimeout(
                () => {
                    pageStates.value[page] = !pageStates.value[page];
                    pageRefs[pages.indexOf(page)].value.style.transform = randomizePageFall();
                    if (index === 2)
                        setTimeout(() => {
                            isAnimationInProgress.value = false;
                        }, 1000);
                },
                20 + 100 * index,
            );
        });
        playSfx(Sfx6);
    }
};

const lastPageZIndex = ref(null);
const updateZIndex = () => {
    lastPageZIndex.value = 30;
    setTimeout(() => {
        lastPageZIndex.value = 'auto';
    }, 1000);
};

const returnPagePosition = () => `rotateZ(0deg) translateY(0%)`;

const toIntroPage = () => {
    if (!isAnimationInProgress.value) {
        isAnimationInProgress.value = true;
        updateZIndex();
        pageStates.value['page7'] = !pageStates.value['page7'];
        pageRefs[pages.indexOf('page7')].value.style.transform = randomizePageFall();
        const pageTransition = 'transform 1s cubic-bezier(0.645, 0.045, 0.355, 1)';
        pages.slice(0, 7).forEach((page) => {
            pageStates.value[page] = !pageStates.value[page];
            pageRefs[pages.indexOf(page)].value.style.transition = 'none';
            pageRefs[pages.indexOf(page)].value.style.transform = returnPagePosition();
            setTimeout(() => {
                pageRefs[pages.indexOf(page)].value.style.transition = pageTransition;
                pageRefs[pages.indexOf('page7')].value.style.transition = 'none';
                pageRefs[pages.indexOf('page7')].value.style.transform = returnPagePosition();
                setTimeout(() => {
                    pageRefs[pages.indexOf('page7')].value.style.transition = pageTransition;
                }, 1000);
                isAnimationInProgress.value = false;
            }, 1000);
        });
    }
};

const isFadeInDone = ref(false);
const isShowTabletDone = ref(false);
const changeWidth = () => {
    if (windowWidth.value <= 1280) isFadeInDone.value = true;
    else isShowTabletDone.value = true;
};

onMounted(() => {
    changeWidth();
    watchEffect(() => {
        if (pageRefs[7].value) {
            pageRefs[7].value.style.zIndex = lastPageZIndex.value;
        }
    });
});
</script>

<style lang="scss">
.background-image {
    @include bg;
    background-image: url('@img/decor/bg-mobile.jpg');
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    min-block-size: 100svb;
    transition: opacity 1s ease-in-out;
    opacity: 0.5;
}
.tablet {
    position: relative;
    @include bg;
    max-width: 36rem;
    width: 100%;
    min-height: 52rem;
    background-color: $c-cover;
    box-shadow: $dc-shadow-card;
    padding-block: $p-10;
    padding-inline: $p-6;
    background-image: url('@img/decor/cover/book-texture.jpg');
    border-radius: $br-8;
    &.show-tablet {
        animation: show 2s forwards;
    }
    &.fade-in {
        animation: fade-in 2s forwards;
    }
    &__overlay {
        box-shadow: 0 0 20px 8px rgba(0, 0, 0, 0.3);
        height: 100%;
    }
    &__clamp {
        @include bg;
        background-image: url('@img/decor/cover/tablet-clamp.png');
        width: 14.5625rem;
        min-height: 6.25rem;
        z-index: 1000;
        position: absolute;
        top: -5%;
        left: 50%;
        transform: translateX(-50%);
    }
    &__page {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        padding-block: $p-10;
        padding-inline: $p-6;
        transition: transform 1s cubic-bezier(0.645, 0.045, 0.355, 1);
        @media (width <= $screen-sm) {
            padding-block: $p-6;
            padding-inline: $p-6;
        }
    }
    &__nav-icon {
        position: absolute;
        fill: lighten(rgb(16, 16, 16), 15%);
        transition: fill $tr-smooth;
        border-radius: $br-circle;
        bottom: 18px;
        right: 18px;
        cursor: pointer;
        &:hover {
            fill: rgb(105, 47, 47);
        }
    }
}
@media (width <= $screen-sm) {
    .tablet {
        max-width: 30rem;
        min-height: 43rem;
        animation: none;
        &__clamp {
            width: 9rem;
            min-height: 3.5rem;
            top: -3%;
        }
        &__nav-icon {
            width: 1.2rem;
            height: 1.2rem;
        }
    }
    .book__page-number {
        font-size: $fs-h6;
        bottom: 16px;
    }
}
@media (width <= $screen-xs) {
    .tablet {
        min-height: 34.3rem;
        &__clamp {
            top: -1.5%;
            width: 5.5625rem;
            min-height: 2.4rem;
        }
    }
}
</style>
