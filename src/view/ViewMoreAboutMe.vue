<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <h1 class="title">More about me</h1>
            <div class="about">
                <p class="about__text">
                    Experienced in building web applications from scratch, solid understanding of
                    modern HTML, CSS, JavaScript, and Vue.js, a knowledge of GIT version control and
                    pull request workflows.
                </p>
                <h2 class="about__subtitle">Additional Info</h2>
                <ul class="about__facts">
                    <li class="about__fact">I'm passionate about learning foreign languages.</li>
                    <li class="about__fact">
                        Practiced eastern martial arts, which taught me discipline and perseverance.
                    </li>
                </ul>
                <h2 class="about__subtitle">Goals</h2>
                <p class="about__text">
                    I'm motivated to build functional, high-quality applications while constantly
                    refining my development skills. I focus on being thorough and results-oriented,
                    always ready to explore new technologies and approaches to achieve the best
                    possible outcomes.
                </p>
            </div>

            <span class="book__page-number">6</span>

            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page3')">
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
import IconBtnDrop from '@/component/icons/IconBtnDrop.vue';
import IconBtnPrev from '@/component/icons/IconBtnPrev.vue';
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
.about {
    display: flex;
    flex-direction: column;
    gap: $g-2;
    margin-top: $m-4;
    &__subtitle {
        font-size: $fs-h6;
        font-weight: 800;
    }
    &__fact {
        list-style: disc;
        margin-left: $p-5;
    }
}

@media (width <= $screen-sm) {
    .about {
        font-size: 0.75rem;
        text-align: justify;
        &__subtitle {
            font-size: $fs-small;
        }
    }
}

@media (width >= $screen-xs) and (width <= $screen-sm) {
    .about {
        font-size: 0.71rem;
        &__subtitle {
            font-size: $fs-small;
        }
    }
}
@media (width <= $screen-xs) {
    .about {
        margin-top: $m-3;
        font-size: 0.59rem;
        &__subtitle {
            font-size: $fs-smaller;
        }
    }
}
</style>
