<template>
    <Page>
        <ActionBar title="Flashcard Vue!"/>
        <FlashCard v-bind:flashcard="flashcards"/>
    </Page>
</template>

<script>
    import FlashCard from './FlashCard.vue';
    import * as http from "http";

    export default {
        data() {
            return {
                flashcards: [{
                    front: "",
                    back: ""
                }],
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
                  this.flashcards = response
                }, error => {
                  console.error(error);
                });
            },
            nextCard: function() {
                if(this.current_card < this.flashcards.length-1) {
                    this.current_card += 1;
                    setCard(this.flashcards[current_card])
                }
            },
            setCard: function(card) {
                this.flashcard = card;
            }
        },
        components: {
            FlashCard
        },
        mounted: function() {
            getCards();

        }

    }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

</style>
