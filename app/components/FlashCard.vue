<template>
    <GridLayout columns="*, 5*, *" rows="*, 3*, *" backgroundColor="#3c495e">
        <Button col=1 row=1 @tap="flip" backgroundColor="#43b883"/>
        <Button col=1 row=1 class=message v-if="!this.flipped" @tap="flip" v-bind:text="flashcard.front" backgroundColor="#43b883" textWrap="true" />
        <Button col=1 row=1 class=message v-if="this.flipped" @tap="flip" v-bind:text=flashcard.back backgroundColor="#43b883" textWrap="true" />
    </GridLayout>
</template>

<script>
  export default {
    props: ['flashcard', 'flipped'],
    methods: {
        flip: function() {
            this.flipped = !this.flipped;
            console.log(this.flashcard);
        }
    }
  }
</script>

<style scoped>
    .message {
        vertical-align: center;
        display: block;
        text-align: center;
        font-size: 15;
        color: #333333;
    }
</style>
