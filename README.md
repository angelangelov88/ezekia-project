I had to create a page using Vue with the following requirements:

1. Cards displaying highlights from the space partners' API should have a different color branding from those in the museum's own data.

2. While in this case the card only needs to work for the Space page, the card component needs to be done in such a way that it would be easily expandable to the other pages. The museum could have X number of pages and they could continually be adding new ones. As a developer, you don't know what those pages might be.

2.1.    Each page has a special badge in the top right corner of the card. This badge is different on every page, and could be an image, or some styled html elements, or a Font Awesome icon. The Space page has an image of a star. The Dinosaur page has a Font Awesome icon inside a circle. The Oceans page has two Font Awesome icons, a wave and a fish together. And so on...

2.2     The data on the different pages (Space, Dinosaurs...) have commonalities but also differences. All highlights have a name, image, date they were posted, a brief description, and perhaps associated news. But all pages also have extra unique data. For example, on the space page, some highlights also include a link to a quiz on the topic. On the dinosaur card, we have a "Period" key to indicate when that dinosaur lived. On the Wildlife page, we have several additional keys: "Location", "Species", and "Endangered status".

3. The cards should be arranged in order of date created, with the most recent first.


My STEPS:

- I displayed the cards using the data from SpacePage.vue data property. I used v-if to make sure there is data or show that no data is available. After that I used v-for directive to display all the data in cards.
- I added 2 separate divs for the cards in order to style them directly depending on the source - local or API.
- I added some props which I add in the MuseumHighlight page and use them in the spacePage component. 
- I made the component as flexible as possible so that it can be used for other pages as well with no much changes.
- I displayed the extra fields from the data property conditionally if they exist like news and quiz.
- I added 2 different badges to the cards top right corner depending on the data source.
- I used SCSS to style the elements and added some extra files such as variable.scss and mixins.scss in order not to repeat my code and make it easier to adjust the code if needed.
- I styled the elements using different colours for the local data cards and API data cards. 
- I used BEM for classes as much as possible but on some occasions I added generic classes so that they can be used for any other page - for example cards, card-container, etc.
- I used lodash to sort the cards based on their date. I sorted them in a descending order so the newest one will be on top.
