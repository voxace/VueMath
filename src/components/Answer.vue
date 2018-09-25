<template>
    <div class="alert alert-success text-center">
        <h1>That's Correct!</h1>
        <hr>
        <button class="btn btn-primary" @click="onNextQuestion">Next Question</button>
    </div>
</template>

<style scoped>
    .alert-success {
        background-color: Green;
        border-color: Black;
        box-shadow: 2px 2px 10px rgba(0,0,0,0.5);
    }

    hr {
        display: block;
        height: 1px;
        border: 0;
        border-top: 1px solid #050;
        margin: 2em 0;
        padding: 0;
    }

    button {
      margin-bottom: 20px;
    }
</style>

<script>

    export default{
        methods: {
            onNextQuestion() {
                this.$emit('confirmed');
            }
        }
    }
</script>
