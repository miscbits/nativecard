<template>
    <Page>
        <ActionBar title="ZC FlashCards">
          <ActionItem text="Next Card" android.systemIcon="Next Card" @tap="nextCard()" />
          <ActionItem text="Shuffle" android.systemIcon="Shuffle" @tap="shuffleDeck()" />
        </ActionBar>
        <FlashCard row=1 col=0 v-bind:flashcard="flashcard" v-bind:flipped="flashcard.flipped"/>
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
                    back: "",
                    flipped: false
                }
            }
        },
        methods: {
            shuffle: function (array) {
              var currentIndex = array.length, temporaryValue, randomIndex;

              // While there remain elements to shuffle...
              while (0 !== currentIndex) {

                // Pick a remaining element...
                randomIndex = Math.floor(Math.random() * currentIndex);
                currentIndex -= 1;

                // And swap it with the current element.
                temporaryValue = array[currentIndex];
                array[currentIndex] = array[randomIndex];
                array[randomIndex] = temporaryValue;
              }

              return array;
            },
            getCards: function() {
                http.request({
                  url: "https://fc.wilhemalcivar.com/api/flashcards",
                  method: "GET",
                  headers: { "Content-Type": "application/json" }
                }).then(response => {
                    this.flashcards = this.shuffle(response.content.toJSON());
                    this.flashcard = this.flashcards[0];
                    this.current_card = 0;
                }, error => {
                    console.log(error)
                });
            },
            nextCard: function() {
                if(this.current_card < this.flashcards.length-1) {
                    this.current_card += 1;
                    var card = this.flashcards[this.current_card];
                    card.flipped = false;
                    this.flashcard = card;
                } else {
                    this.flashcard = {
                        front: "Last card. Click shuffle to start over",
                        back: "Last card. Click shuffle to start over",
                        flipped: false
                    }
                }
            },
            onLoaded: function() {
                this.getCards();
            }, 
            shuffleDeck: function() {
                this.flashcards = this.shuffle(this.flashcards);
                this.flashcard = this.flashcards[0];
                this.current_card = 0;
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
