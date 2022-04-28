This task is spread between two vue components.

GENERAL GUIDELINES

- Use ES6 notation
- Use SCSS
- Use BEM for classes if possible
- Using Lodash would make some functions a lot easier! (https://lodash.com/docs/4.17.15)
- We've added a bit of code for context, do what you want with it. Feel free to modify or move if you think something else is better. However, please do not modify the arrays/objects in "data()"
- We do not expect things to be working fully or look perfect but the code added and the approach need to make sense, and there needs to be some evidence that user experience was considered
- If at any point you want to do something but you do not have a package imported, just mock it out in the code as best you can and/or put a comment about what you would have done if you'd had the package available.



CONTEXT

You manage a natural history museum website. The museum has a set of web pages, each with a theme, and containing a list of that theme's highlights within the museum's exhibits. These pages include Dinosaurs, Space, Oceans, and Wildlife.

For example:
On the Space page, you have a list of cards, each with a space-related subject found in the museum, like asteroids, comets, black holes, stars, etc...
On the Dinosaur page, you have a list of cards, each with a dinosaur referencing fossils found in the museum.
On the Wildlife page, you have a list of cards, each with an animal.

The museum also works with partners and has set up an API where the museum website receives data related to one of these pages. For example, the museum partners with an observatory in Hawaii and receives some Space highlights from them that need to be mixed in with the museum's own data.

In the email, there should also be a basic sketch of what the Space page would look like, if that helps to visualize!



YOUR GOAL

Display the Space page highlights on cards in a list using the museum's data combined with data from the partner's API. Sample data is found in "Data()" and since we don't have any backend, pretend it was loaded in. Also to keep it simple, there are only a few highlights there, but there could be hundreds. Note: The data is intentionally in different formats.



REQUIREMENTS

1. Cards displaying highlights from the space partners' API should have a different color branding from those in the museum's own data.

2. While in this case the card only needs to work for the Space page, the card component needs to be done in such a way that it would be easily expandable to the other pages. The museum could have X number of pages and they could continually be adding new ones. As a developer, you don't know what those pages might be.

2.1.    Each page has a special badge in the top right corner of the card. This badge is different on every page, and could be an image, or some styled html elements, or a Font Awesome icon. The Space page has an image of a star. The Dinosaur page has a Font Awesome icon inside a circle. The Oceans page has two Font Awesome icons, a wave and a fish together. And so on...

2.2     The data on the different pages (Space, Dinosaurs...) have commonalities but also differences. All highlights have a name, image, date they were posted, a brief description, and perhaps associated news. But all pages also have extra unique data. For example, on the space page, some highlights also include a link to a quiz on the topic. On the dinosaur card, we have a "Period" key to indicate when that dinosaur lived. On the Wildlife page, we have several additional keys: "Location", "Species", and "Endangered status".

3. The cards should be arranged in order of date created, with the most recent first.


Follow the requirements and also complete any prompts in the two component files. You can return these two files with the content filled in, or copy and paste the relevant code and create something on Github, or in JSFiddle.



<template>
    <div class="space-page">
        <h1 class="space-page__title">
            {{ title }}
        </h1>
        <!-- Add the museum highlight cards based on the data provided below -->
        <div v-if="spaceHighlights.length || spacePartners.length" class="cards-main">
            <div class="cards-container">
                <div v-for="item in sortByDate(spaceHighlights)" :key="item.id" class="cards">
                    <i class="space-page__star"></i>
                    <img :src="item.image" :alt="item.name" class="images">
                    <h2>{{ item.name }}</h2>
                    <p>{{ item.description }}</p>
                    <div v-if="item.news">
                        <h5 class="space-page__news--text">{{ cardItem1 }}:</h5> 
                        <p class="space-page__news--title">{{ item.news.title }}</p>
                    </div>
                    <div v-if="item.quiz">
                        <h5 class="space-page__quiz--text">{{ cardItem2 }}:</h5> 
                        <a :href="item.quiz" v-if="item.quiz" class="space-page__quiz--link links">Click here for a quick quiz on the topic</a>
                    </div>
                </div>
            </div>
            <div class="cards-container">
                <div v-for="(item, id) in spacePartners" :key="id" class="cards-partners">
                    <i><span class="space-page__sun"></span></i>
                    <img :src="item.image" :alt="item.name" class="images">
                    <h2>{{ item.name }}</h2>
                    <p>{{ item.info }}</p>
                </div>
            </div>
        </div>
        <div v-else>No data is available</div>
    </div>
</template>

<script>

import MuseumHighlight from './MuseumHighlight';
import lodash from 'lodash'

export default {
    name: 'SpacePage',
    components: {
        MuseumHighlight,
    },
    mixins: [
    ],
    props: [
        'title',
        'cardItem1',
        'cardItem2',
    ],
    data() {
        return {
            spaceHighlights: [
                {
                    date: '2020-04-20 12:20:00',
                    description: 'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
                    id: 1,
                    image: 'https://cdn.mos.cms.futurecdn.net/E7wi2UxqcuH6rj8kCe7WnA-1024-80.jpg.webp',
                    name: 'Asteroids',
                },
                {
                    date: '2020-05-20 15:50:00',
                    description: 'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
                    id: 9,
                    image: 'https://cdn.mos.cms.futurecdn.net/E7wi2UxqcuH6rj8kCe7WnA-1024-80.jpg.webp',
                    name: 'Comets',
                },
                {
                    date: '2020-05-01 9:22:00',
                    description: 'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
                    id: 7,
                    image: 'https://cdn.mos.cms.futurecdn.net/E7wi2UxqcuH6rj8kCe7WnA-1024-80.jpg.webp',
                    name: 'Planets',
                    news: {
                        date: '2020-08-18 18:00:00',
                        title: 'Attend our talk about Jupiter with Dr. Hogarth',
                    },
                    quiz: 'https://planetquiz.space',
                },
                {
                    date: '2020-07-05 4:10:00',
                    description: 'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
                    id: 12,
                    image: 'https://cdn.mos.cms.futurecdn.net/E7wi2UxqcuH6rj8kCe7WnA-1024-80.jpg.webp',
                    name: 'Meteor showers',
                    news: {
                        title: 'The Lyrids will peak at on April 21-22 2021, at night',
                    },
                },
            ],
            spacePartners: {
                observatory: {
                    createdAt: '2020-06-01 11:45:00',
                    info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
                    image: 'https://media.tacdn.com/media/attractions-splice-spp-674x446/0b/27/54/e0.jpg',
                    name: 'Mauna Kea Observatories',
                },
            },
        };
    },
    computed: {        

    },
    methods: {
        sortByDate: (spaceHighlights) => {
            return _.orderBy(spaceHighlights, 'date', 'desc')
        }
    },
    created() {

    },
};
</script>

<style lang="scss" scoped>
@import '../assets/styles/mixins.scss';
@import '../assets/styles/variables.scss';

.space-page {
//I have used BEM for the classes in .space-page
    &__title {
        color: #2c3791;
        font-size: 24px;
        font-weight: 600;
    }
    &__news--text , 
    &__quiz--text {
        margin-bottom: 0;
        color: gray;
    }
    &__news--title,
    &__quiz--link {
        margin-top: 0
    }
//I added the star and sun as different icons for the 2 types of cards - local and API. They are just HTML elements styled in CSS
    &__star {
    @include badge-positioning;
    width: 0;
    height: 0;
    margin-left: .9em;
    margin-right: .9em;
    margin-bottom: 1.2em;
    border-right:  .3em solid transparent;
    border-bottom: .7em  solid #FC0;
    border-left:   .3em solid transparent;
//Controlls the size of the stars. 
    font-size: 24px;
    &:before, &:after {
    content: '';
        display: block;
        width: 0;
        height: 0;
        position: absolute;
        top: .6em;
        left: -1em;
        border-right:  1em solid transparent;
        border-bottom: .7em  solid #FC0;
        border-left:   1em solid transparent;
        transform: rotate(-35deg);
    }
    &:after {  
        transform: rotate(35deg);
}
}
    &__sun {
        @include badge-positioning;
        --color1: #f1bd00;
        --color2: #fbf26e;
        --colorbg: #edc61c;
    }
    &__sun,
    &__sun::before,
    &__sun::after {
        width: 40px;
        height: 40px;
        background: radial-gradient(
        circle,
        var(--colorbg) 0%,
        var(--colorbg) 65%,
        var(--color2) 66%,
        var(--color1) 100%
        );
        --deg: 45deg;
        transform: rotatez(var(--deg));
        animation-name: moving;
        animation-duration: 5.5s;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
    }
    &__sun::before,
    &__sun::after {
        content: "";
        position: absolute;
        --deg: 60deg;
        transform: rotatez(var(--deg));
        top: 0;
        left: 0;
        animation-delay: 0.3s;
    }
    &__sun::after {
        --deg: -60deg;
        transform: rotatez(var(--deg));
        animation-delay: 0.6s;
}
}

//I decided to add those classes as separate ones not part of the .space-page one because they can be used for any other element. I know that the scoped property at the top would not allow that to happen currently but it can be easily removed or this code can be added to another page where to take effect from for all other pages as well
.cards-main {
    display: flex;
    flex-direction: column
}

.cards-container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

.cards {
    @include cards;
        background-color: $brand-green-colour;
}

.cards:hover {
    background-color: white;
    color: darken($color: $brand-green-colour, $amount: 30%);
    border: 10px $brand-green-colour solid;
}

.images {
    width: 250px;
    height: 150px;
    margin-bottom: -15px;
}

.cards-partners {
    @include cards;
    background-color: $brand-yellow-colour;
}

.cards-partners:hover{
    background-color: white;
    color: darken($color: $brand-yellow-colour, $amount: 10);
    border: 10px $brand-yellow-colour solid;
}



</style>
