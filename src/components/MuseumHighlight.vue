<template>
    <div class="museum-highlight">
        <!-- Display the available information for the highlight -->
        <header class="header">
            <div class="header__left-items">
                <img class="header__globe" src="../../public/globe.png" alt="globe-logo">
                <h2>Natural History Museum</h2>
            </div>
            <div class="header__hamburger">
                <div class="header__menu-lines">
                    <div class="header__menu-line"></div>
                    <div class="header__menu-line header__menu-line-2"></div>
                    <div class="header__menu-line"></div>	
                </div>
            </div>
        </header>
        <SpacePage 
            :title="title"
            :cardItem1="cardItem1"  
            :cardItem2="cardItem2"  
         />
    </div>
</template>

<script>
import SpacePage from './SpacePage.vue'

export default {
    name: 'MuseumHighlight',
    components: {
        SpacePage,
    },
    mixins: [
    ],
    props: {

    },
    data() {
        return {
            title: 'Space',
            cardItem1: "NEWS",
            cardItem2: "QUIZ"
        };
    },
    computed: {
        newsDate() {
            // Highlight's news item date
        },
    },
    methods: {

    },
    created() {

    },
};
</script>

<style lang="scss" scoped>

.header {
    background-color: #F7F7F7;
    display: flex;
    justify-content: space-between;
    &__left-items {
        display: flex;
    }
    &__globe {
        margin: 10px 20px;
        width: 62px;
        height: auto;
    }
    &__hamburger {
        margin: 10px 20px 10px 10px;
        cursor: pointer;
    }
    &__menu-lines {
        padding: 6px 0 5px 6px;
    }
    &__menu-line {
        width: 30px;
        height: 8px;
        margin-bottom: 2px;
        background-color: black;
        border-radius: 5px;
    }
    &__menu-line-2 {
        width: 38px;
    }
}

</style>
