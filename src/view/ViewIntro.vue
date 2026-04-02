<template>
    <div class="book__overlay book__overlay--left" v-if="windowWidth > 1280"></div>
    <div class="book__content book__content--left">
        <div class="book__content-inner">
            <div class="profile">
                <div class="profile__avatar"></div>
                <div class="profile__name">Mykhailo Prysiazhnyi</div>
                <div class="profile__specialization">Frontend &nbsp;&nbsp;Developer</div>
                <ul class="profile__social">
                    <li>
                        <a
                            class="profile__social-link"
                            href="https://www.linkedin.com/"
                            target="_blank">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                                <circle cx="4.983" cy="5.009" r="2.188"></circle>
                                <path
                                    d="M9.237 8.855v12.139h3.769v-6.003c0-1.584.298-3.118 2.262-3.118 1.937 0 1.961 1.811 1.961 3.218v5.904H21v-6.657c0-3.27-.704-5.783-4.526-5.783-1.835 0-3.065 1.007-3.568 1.96h-.051v-1.66H9.237zm-6.142 0H6.87v12.139H3.095z"></path>
                            </svg>
                        </a>
                    </li>
                    <li>
                        <a
                            class="profile__social-link"
                            href="https://github.com/michaelprys"
                            target="_blank">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                                <path
                                    fill-rule="evenodd"
                                    clip-rule="evenodd"
                                    d="M12.026 2c-5.509 0-9.974 4.465-9.974 9.974 0 4.406 2.857 8.145 6.821 9.465.499.09.679-.217.679-.481 0-.237-.008-.865-.011-1.696-2.775.602-3.361-1.338-3.361-1.338-.452-1.152-1.107-1.459-1.107-1.459-.905-.619.069-.605.069-.605 1.002.07 1.527 1.028 1.527 1.028.89 1.524 2.336 1.084 2.902.829.091-.645.351-1.085.635-1.334-2.214-.251-4.542-1.107-4.542-4.93 0-1.087.389-1.979 1.024-2.675-.101-.253-.446-1.268.099-2.64 0 0 .837-.269 2.742 1.021a9.582 9.582 0 0 1 2.496-.336 9.554 9.554 0 0 1 2.496.336c1.906-1.291 2.742-1.021 2.742-1.021.545 1.372.203 2.387.099 2.64.64.696 1.024 1.587 1.024 2.675 0 3.833-2.33 4.675-4.552 4.922.355.308.675.916.675 1.846 0 1.334-.012 2.41-.012 2.737 0 .267.178.577.687.479C19.146 20.115 22 16.379 22 11.974 22 6.465 17.535 2 12.026 2z"></path>
                            </svg>
                        </a>
                    </li>
                    <li>
                        <a
                            class="profile__social-link"
                            href="https://stackoverflow.com/users/20343913"
                            target="_blank">
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                                <path
                                    d="M17.24 19.399v-4.804h1.6V21H4.381v-6.405h1.598v4.804H17.24zM7.582 17.8h8.055v-1.604H7.582V17.8zm.195-3.64 7.859 1.641.34-1.552-7.861-1.642-.338 1.553zm1.018-3.794 7.281 3.398.678-1.463-7.281-3.399-.678 1.454v.01zm2.037-3.589 6.166 5.142 1.018-1.216-6.162-5.14-1.016 1.213-.006.001zm3.982-3.778-1.311.969 4.803 6.454 1.313-.971-4.807-6.452h.002z"></path>
                            </svg>
                        </a>
                    </li>
                </ul>
                <div class="profile__about">
                    Developing responsive web applications with Vue.js, TypeScript, and modern CSS.
                    I aim to build clean, functional interfaces while constantly improving my
                    technical skills through applied practice.
                </div>
                <div class="profile__buttons">
                    <a class="profile__link" :href="cvLink" target="_blank">Resume</a>
                    <button type="button" class="profile__button" @click="toLastPage()">
                        Contact
                    </button>
                </div>
            </div>
            <TurnButton v-if="windowWidth <= 1280" @click="dropPage()">
                <IconBtnDrop />
            </TurnButton>
        </div>
    </div>
</template>

<script setup>
import TurnButton from '@/component/TurnButton.vue';
import IconBtnDrop from '@/component/icons/IconBtnDrop.vue';
import { useWindowSize } from '@vueuse/core';

const { width: windowWidth } = useWindowSize();

defineProps(['dropPage', 'toLastPage']);

const cvLink = import.meta.env.VITE_CV_URL;
</script>

<style lang="scss">
.profile {
    display: flex;
    flex-direction: column;
    text-align: center;
    position: relative;
    &__avatar {
        position: relative;
        @include bg;
        background-image: url('@img/decor/profile/avatar.webp');
        margin-inline: auto;
        width: 12.5rem;
        height: 12.5rem;
        border-radius: $br-6;
        filter: grayscale(88%) hue-rotate(340deg) brightness(95%) contrast(95%);
        background-size: auto 158%;
        background-position: top;

        border: 4px solid #4b4a3a;
        outline: 1px solid #323129;
        outline-offset: -1px;

        box-shadow:
            inset 0 0 15px rgba(0, 0, 0, 0.7),
            2px 2px 8px rgba(0, 0, 0, 0.3);

        &::before {
            content: '';
            position: absolute;
            inset: -3px;
            background-image:
                radial-gradient(circle, #666 0.8px, transparent 1.5px),
                radial-gradient(circle, #666 0.8px, transparent 1.5px),
                radial-gradient(circle, #666 0.8px, transparent 1.5px),
                radial-gradient(circle, #666 0.8px, transparent 1.5px);
            background-position:
                1px 1px,
                calc(100% - 1px) 1px,
                1px calc(100% - 1px),
                calc(100% - 1px) calc(100% - 1px);
            background-repeat: no-repeat;
            background-size: 5px 5px;
            pointer-events: none;
        }

        &::after {
            content: '';
            position: absolute;
            inset: 0;
            background: linear-gradient(
                135deg,
                rgba(255, 255, 255, 0.03) 0%,
                transparent 50%,
                rgba(0, 0, 0, 0.08) 100%
            );
            pointer-events: none;
        }
    }
    &__name {
        margin-top: $m-3_5;
        font-size: 2.75rem;
        font-family: $ff-secondary;
    }
    &__specialization {
        position: relative;
        color: $c-text;
        font-size: $fs-base;
        margin-inline: auto;
        font-family: $ff-secondary;
        font-size: 1.75rem;
        margin-top: $m-2;
        &::before {
            position: absolute;
            top: -15%;
            transform: translateX(-50%);
            left: 50%;
            content: '';
            width: 110%;
            height: 1px;
            background-color: rgba($c-cover, 30%);
        }
    }
    &__social {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: $g-5;
    }
    &__social-link {
        width: 2.3rem;
        height: 2.3rem;
        transition: fill $tr-smooth;
        fill: $c-text;
        border-radius: $br-circle;
        outline: 2px solid transparent;
        padding: 5px;
        &:hover {
            fill: $c-cover;
        }
    }
    &__about {
        text-align: justify;
        margin-top: $m-5;
        font-family: $ff-primary-italic;
        font-size: $fs-base;
    }
    &__buttons {
        display: flex;
        justify-content: center;
        gap: $g-8;
        margin-top: $m-10;
    }
    &__link,
    &__button {
        @include btn-big;
        padding-block: $p-2;
        padding-inline: $p-4;
    }
}

@media (width <= $screen-sm) {
    .profile {
        &__avatar {
            width: 11rem;
            height: 11rem;
        }
        &__name {
            font-size: $fs-h1;
        }
        &__specialization {
            font-size: $fs-h4;
        }
        &__about {
            font-size: $fs-smaller;
            margin-top: $m-2_5;
        }
        &__buttons {
            padding-inline: $p-12;
        }
        &__link,
        &__button {
            min-width: $w-20;
        }
    }
}
@media (width >= $screen-xs) and (width <= $screen-sm) {
    .profile {
        &__social-link {
            width: 2rem;
            height: 2rem;
        }
        &__name {
            font-size: $fs-h2;
        }
        &__specialization {
            font-size: $fs-h5;
        }
        &__buttons {
            margin-top: $m-5;
        }
        &__link,
        &__button {
            min-width: $w-16;
            font-size: 0.75rem;
        }
    }
}

@media (width <= $screen-xs) {
    .profile {
        &__avatar {
            width: 9rem;
            height: 8rem;
        }
        &__name {
            font-size: $fs-h3;
        }
        &__specialization {
            font-size: $fs-h5;
        }
        &__social-link {
            width: 1.8rem;
            height: 1.8rem;
        }
        &__about {
            font-size: $fs-smaller;
        }

        &__buttons {
            padding-inline: $p-6;
            margin-top: $m-5;
        }
        &__link,
        &__button {
            min-width: $w-16;
            font-size: 0.75rem;
            padding-block: $p-1_5;
        }
    }
}
</style>
