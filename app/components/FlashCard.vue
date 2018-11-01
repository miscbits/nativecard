<template>
    <GridLayout columns="*, 5*, *" rows="*, 3*, *" backgroundColor="#3c495e">
        <Label col=1 row=1 backgroundColor="#43b883"/>
        <Label col=1 row=1 class=message v-bind:text=flashcard.front backgroundColor="#43b883"/>
    </GridLayout>
</template>

<script>
  export default {
    data() {
      return {
        flashcard: this.flashcard,
        flipped: false
      }
    },
    props: ['flashcard'],
    methods: {
        reset: function() {
            this.flipped = false;
        },
        flip: function() {
            this.flipped = !this.flipped;
        }

    }
  }
</script>

<style scoped>
    .message {
        vertical-align: center;
        display: block;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
</style>
