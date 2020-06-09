<template>
    <div class="answer">
        <div class="answer__inner">
            <div class="answer__text">
                <h1>That's correct</h1>
                <button class="btn" @click="onNextQuestion">Next Questioin</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        onNextQuestion() {
            this.$emit('confirmed')
        }
    }
}
</script>

<style lang="scss" scoped>
    .answer{
        border: 3px solid #00ffff;
        background-color: rgb(213, 255, 249);
        text-align: center;

        & h1 {
            border-bottom: 3px solid  #00ffff;
            margin: 10px 0;
            color:#005858;
        }

        & .btn {
            margin-top: 40px;
            padding: 5px 10px;
            background: #005858;
            color: #fff;
            box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.678);
            border-radius: 5px;

            &:hover {
                box-shadow: none;
                transform: translate(3px, 3px)
            }
        }
    }
</style>