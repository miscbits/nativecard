<template>
    <GridLayout columns="*, 5*, *" rows="*, 3*, *" backgroundColor="#3c495e">
        <Button col=1 row=1 @tap="flip" backgroundColor="#43b883"/>
        <Button col=1 row=1 class=message v-if="!flipped" @tap="flip" v-bind:text="flashcard.front" backgroundColor="#43b883"/>
        <Button col=1 row=1 class=message v-if="flipped" @tap="flip" v-bind:text=flashcard.back backgroundColor="#43b883"/>
    </GridLayout>
</template>

<script>
  export default {
    data() {
      return {
        flipped: false
      }
    },
    props: ['flashcard'],
    methods: {
        reset: function() {
            this.flipped = false
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
