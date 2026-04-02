<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <div class="experience">
                <h1 class="title title--about">Experience</h1>
                <div class="experience__item">
                    <span class="year">
                        <IconCalendar />
                        2024 – present
                    </span>
                    <h2 class="subtitle">
                        Frontend Developer
                        <span class="subtitle__years">(2+ Years)</span>
                    </h2>
                    <ul class="experience__list">
                        <li>Creating interactive interfaces with Vue, Pinia, and Quasar.</li>
                        <li>Writing reliable code with TypeScript and handling API data.</li>
                        <li>Creating modular UI components to simplify maintenance.</li>
                        <li>Implementing modern web standards and responsive layouts.</li>
                    </ul>
                </div>
                <div class="experience__item">
                    <span class="year">
                        <IconCalendar />
                        2017 – Present
                    </span>
                    <h2 class="subtitle">
                        Digital Producer
                        <span class="subtitle__years">(9 Years)</span>
                    </h2>
                    <ul class="experience__list">
                        <li>Digital Product Delivery & Operations.</li>
                        <li>Proven track record in Product Ownership.</li>
                        <li>End-to-end management from concept to market launch.</li>
                        <li>Autonomous workflow in sync with product vision.</li>
                    </ul>
                </div>
            </div>
            <div class="communication">
                <h1 class="title title--about">Communication</h1>
                <div class="subtitle subtitle--languages">Languages</div>
                <ul class="communication__grid">
                    <li>English (Advanced)</li>
                    <li>Czech (Intermediate)</li>
                    <li>Spanish (Upper-Int.)</li>
                    <li>Ukrainian (Native)</li>
                    <li>Russian (Native)</li>
                </ul>
            </div>
            <span class="book__page-number">1</span>
            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page1')">
                <IconBtnNext />
            </TurnButton>
            <IconBtnDrop v-else class="tablet__nav-icon" @click="dropPage('page1')" />
        </div>
    </div>
</template>

<script setup>
import TurnButton from '@/component/TurnButton.vue';
import IconBtnDrop from '@/component/icons/IconBtnDrop.vue';
import IconBtnNext from '@/component/icons/IconBtnNext.vue';
import IconCalendar from '@/component/icons/IconCalendar.vue';
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
.experience {
    &__item {
        margin-bottom: $m-3;
    }
    &__list {
        padding-left: $p-5;
        list-style: disc;
        li {
            margin-bottom: $m-1;
            font-size: $fs-medium;
            line-height: 1.4;
        }
    }
}
.communication {
    margin-top: $m-4;
    &__grid {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: $g-1 $g-4;
        padding-left: $p-5;
        li {
            list-style: disc;
            font-size: $fs-medium;
        }
    }
}
.subtitle {
    margin: $m-1 0;
    font-size: $fs-h6;
    font-weight: $fw-bold;
    &--languages {
        margin-bottom: 4px;
    }
    &__years {
        font-weight: $fw-regular;
    }
}
.year {
    display: flex;
    align-items: center;
    gap: $g-2;
    font-family: $ff-primary-italic;
    font-size: $fs-base;
    svg {
        width: $w-4;
        height: $h-4;
    }
}

.tablet__nav-icon {
    background: transparent !important;
    border: none !important;
    box-shadow: none !important;
    outline: none !important;
    -webkit-tap-highlight-color: transparent;
    padding: 0;
}

@media (width <= $screen-sm) {
    .experience__item {
        margin-bottom: 6px;
    }
    .experience__list li,
    .communication__grid li {
        font-size: 0.75rem;
        line-height: 1.2;
    }
    .subtitle {
        font-size: 0.85rem;
        margin: 2px 0;
    }
    .title--about {
        font-size: 1rem;
        margin-bottom: 6px;
    }
    .communication {
        margin-top: 8px;
    }
}
</style>
