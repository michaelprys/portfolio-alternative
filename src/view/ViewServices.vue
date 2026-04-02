<template>
    <div class="book__content book__content--right">
        <div class="book__content-inner">
            <h1 class="title">Services</h1>
            <ul class="services">
                <li class="services__item">
                    <svg
                        class="services__icon"
                        xmlns="http://www.w3.org/2000/svg"
                        width="1.5rem"
                        height="1.5rem"
                        viewBox="0 0 24 24">
                        <path
                            d="m7.375 16.781 1.25-1.562L4.601 12l4.024-3.219-1.25-1.562-5 4a1 1 0 0 0 0 1.562l5 4zm9.25-9.562-1.25 1.562L19.399 12l-4.024 3.219 1.25 1.562 5-4a1 1 0 0 0 0-1.562l-5-4zm-1.649-4.003-4 18-1.953-.434 4-18z"></path>
                    </svg>
                    <span class="services__title">Intelligent Features</span>
                    <p class="services__text">
                        Connecting applications with AI models and geolocation services to enhance
                        user interactivity.
                    </p>
                </li>
                <li class="services__item">
                    <svg
                        class="services__icon"
                        xmlns="http://www.w3.org/2000/svg"
                        width="1.5rem"
                        height="1.5rem"
                        viewBox="0 0 24 24">
                        <path
                            d="M20 3H7c-1.103 0-2 .897-2 2v2H4c-1.103 0-2 .897-2 2v10c0 1.103.897 2 2 2h6c1.103 0 2-.897 2-2h8c1.103 0 2-.897 2-2V5c0-1.103-.897-2-2-2zM9.997 19H4V9h6l-.003 10zm10-2H12V9c0-1.103-.897-2-2-2H7V5h13l-.003 12z"></path>
                    </svg>
                    <span class="services__title">Dynamic Layouts & UX</span>
                    <p class="services__text">
                        Optimizing perceived performance with skeleton loaders, efficient state
                        handling, and responsive layouts.
                    </p>
                </li>
                <li class="services__item">
                    <svg
                        class="services__icon"
                        xmlns="http://www.w3.org/2000/svg"
                        width="1.5rem"
                        height="1.5rem"
                        viewBox="0 0 24 24">
                        <path
                            d="M12 16c2.206 0 4-1.794 4-4s-1.794-4-4-4-4 1.794-4 4 1.794 4 4 4zm0-6c1.084 0 2 .916 2 2s-.916 2-2 2-2-.916-2-2 .916-2 2-2z"></path>
                        <path
                            d="m2.845 16.136 1 1.73c.531.917 1.809 1.261 2.73.73l.529-.306A8.1 8.1 0 0 0 9 19.402V20c0 1.103.897 2 2 2h2c1.103 0 2-.897 2-2v-.598a8.132 8.132 0 0 0 1.896-1.111l.529.306c.923.53 2.198.188 2.731-.731l.999-1.729a2.001 2.001 0 0 0-.731-2.732l-.505-.292a7.718 7.718 0 0 0 0-2.224l.505-.292a2.002 2.002 0 0 0 .731-2.732l-.999-1.729c-.531-.92-1.808-1.265-2.731-.732l-.529.306A8.1 8.1 0 0 0 15 4.598V4c0-1.103-.897-2-2-2h-2c-1.103 0-2 .897-2 2v.598a8.132 8.132 0 0 0-1.896 1.111l-.529-.306c-.924-.531-2.2-.187-2.731.732l-.999 1.729a2.001 2.001 0 0 0 .731 2.732l.505.292a7.683 7.683 0 0 0 0 2.223l-.505.292a2.003 2.003 0 0 0-.731 2.733zm3.326-2.758A5.703 5.703 0 0 1 6 12c0-.462.058-.926.17-1.378a.999.999 0 0 0-.47-1.108l-1.123-.65.998-1.729 1.145.662a.997.997 0 0 0 1.188-.142 6.071 6.071 0 0 1 2.384-1.399A1 1 0 0 0 11 5.3V4h2v1.3a1 1 0 0 0 .708.956 6.083 6.083 0 0 1 2.384 1.399.999.999 0 0 0 1.188.142l1.144-.661 1 1.729-1.124.649a1 1 0 0 0-.47 1.108c.112.452.17.916.17 1.378 0 .461-.058.925-.171 1.378a1 1 0 0 0 .471 1.108l1.123.649-.998 1.729-1.145-.661a.996.996 0 0 0-1.188.142 6.071 6.071 0 0 1-2.384 1.399A1 1 0 0 0 13 18.7l.002 1.3H11v-1.3a1 1 0 0 0-.708-.956 6.083 6.083 0 0 1-2.384-1.399.992.992 0 0 0-1.188-.141l-1.144.662-1-1.729 1.124-.651a1 1 0 0 0 .471-1.108z"></path>
                    </svg>
                    <span class="services__title">Solid App Foundation</span>
                    <p class="services__text">
                        Building robust SPAs with structured state management, secure routing, and
                        scalable component logic.
                    </p>
                </li>
            </ul>
            <span class="book__page-number">2</span>

            <TurnButton v-if="windowWidth > 1280" @click="handleTurnPage('page1')">
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
.services {
    margin-top: $m-10;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: $g-7;

    &__item {
        border-radius: $br-8;
        padding: $p-4;
        box-shadow: $dc-shadow-inner;
        transition: box-shadow $tr-smooth;
        &:hover {
            box-shadow: 0 0 0.8rem rgba(0, 0, 0, 0.3);
        }
    }
    &__title {
        display: block;
        text-align: center;
        font-weight: bold;
        font-size: $fs-small;
        margin-block: $m-2_5;
    }
    &__text {
        font-size: $fs-medium;
        line-height: 1.4;
        text-align: center;
        text-wrap: balance;
        hyphens: auto;
        margin-inline: auto;
    }
    &__icon {
        fill: $c-text;
        margin-inline: auto;
    }
}

@media (width <= $screen-sm) {
    .services {
        margin-top: $m-6;
        &__item {
            padding: $p-3;
        }
        &__title {
            font-size: 0.75rem;
        }
        &__text {
            font-size: 0.8125rem;
        }
        &__icon {
            width: 1.5rem;
            height: 1.5rem;
        }
    }
}

@media (width >= $screen-xs) and (width <= $screen-sm) {
    .services {
        gap: $g-4;
        &__title {
            font-size: 0.65rem;
        }
        &__text {
            font-size: 0.75rem;
        }
    }
}

@media (width <= $screen-xs) {
    .services {
        gap: $g-3;
        margin-top: $m-5;
        grid-template-columns: 1fr;
        &__item {
            padding: $p-2;
        }
        &__title {
            font-size: 0.65rem;
        }
        &__text {
            font-size: 0.675rem;
        }
        &__icon {
            width: 1.2rem;
            height: 1.2rem;
        }
    }
}
</style>
