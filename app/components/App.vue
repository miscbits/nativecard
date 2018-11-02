<template>
    <Page>
        <ActionBar title="FlashCard Vue">
          <ActionItem text="Next Card" android.systemIcon="Next Card" @tap="nextCard" />
        </ActionBar>
        <FlashCard row=1 col=0 v-bind:flashcard="flashcard"/>
    </Page>
</template>

<script>
    import FlashCard from './FlashCard.vue';
    const http = require("http");
    import * as app from 'tns-core-modules/application'

    export default {
        data() {
            return {
                flashcards: this.getCards(),
                current_card: 0,
                flashcard: {
                    front: "",
                    back: ""
                }
            }
        },
        methods: {
            getCards: function() {
                http.request({
                  url: "https://fc.wilhemalcivar.com/api/flashcards",
                  method: "GET",
                  headers: { "Content-Type": "application/json" }
                }).then(response => {
                    this.flashcards = response.content.toJSON();
                    this.flashcard = this.flashcards[0];
                    this.current_card = 0;
                }, error => {
                    console.log(error)
                });
            },
            nextCard: function() {
                if(this.current_card < this.flashcards.length-1) {
                    this.current_card += 1;
                    setCard(this.flashcards[this.current_card])
                }
            },
            setCard: function(card) {
                this.flashcard = card;
            },
            onLoaded: function() {
                this.getCards();
            }
        },
        components: {
            FlashCard
        },

    }

</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

</style>
