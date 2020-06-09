<template>
    <div class="question">
        <div class="question__title">
            <h3>{{ question }}</h3>
        </div>
        <div class="question__content">
            <div class="question__text">
                <button class="btn" @click="onAnswer(btnData[0].correct)">
                    {{ btnData[0].answer }}
                </button>
            </div>
            <div class="question__text">
                <button class="btn" @click="onAnswer(btnData[1].correct)">
                    {{ btnData[1].answer }}
                </button>
            </div>
            <div class="question__text">
                <button class="btn" @click="onAnswer(btnData[2].correct)">
                    {{ btnData[2].answer }}
                </button>
            </div>
            <div class="question__text">
                <button class="btn" @click="onAnswer(btnData[3].correct)">
                    {{ btnData[3].answer }}
                </button>
            </div>
        </div>
    </div>
</template>

<script>
const MODE_ADDITION = 1;
const MODE_SUBTRACTION = 2;
export default {
    data() {
        return {
            question: '0ops an Error occurred :/',
            btnData: [
                {
                    correct: true,
                    answer: 0,
                },
                {
                    correct: false,
                    answer: 0,
                },
                {
                    correct: false,
                    answer: 0,
                },
                {
                    correct: false,
                    answer: 0,
                },

            ],
        }
    },
    methods: {
        generateQuestion() {
            const firstNumber = this.genetateRandomNumber(1, 100);
            const secondNumber = this.genetateRandomNumber(1, 100);
            const modeNumber = this.genetateRandomNumber(1, 2);
            
            let correctAnswer = 0;

            switch (modeNumber) {
                case MODE_ADDITION:
                    correctAnswer = firstNumber + secondNumber;
                    this.question = `What's ${firstNumber} + ${secondNumber}?`;
                    break;
                case MODE_SUBTRACTION:
                    correctAnswer = firstNumber - secondNumber;
                    this.question = `What's ${firstNumber} - ${secondNumber}?`;
                    break;
                default:
                    correctAnswer = 0;
                    this.question = '0ops an Error occurred :/'
            }

            this.btnData[0].answer = this.genetateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
            this.btnData[0].correct = false;
            this.btnData[1].answer = this.genetateRandomNumber(correctAnswer - 20, correctAnswer + 20, correctAnswer);
            this.btnData[1].correct = false;
            this.btnData[2].answer = this.genetateRandomNumber(correctAnswer - 13, correctAnswer + 13, correctAnswer);
            this.btnData[2].correct = false;
            this.btnData[3].answer = this.genetateRandomNumber(correctAnswer - 15, correctAnswer + 15, correctAnswer);
            this.btnData[3].correct = false;

            const correctButton = this.genetateRandomNumber(0, 3);
            this.btnData[correctButton].correct = true;
            this.btnData[correctButton].answer = correctAnswer;
        },
        genetateRandomNumber(min, max, except) {
            const rndNumber = Math.round(Math.random() * (max - min)) + min;
            console.log(min, max, except);
            if (rndNumber == except) {
                return this.genetateRandomNumber(min, max, except);
            }
            return rndNumber;
        },
        onAnswer(isCorrect) {
            this.$emit('answered',isCorrect)
        },
    },
    created() {
        this.generateQuestion();
    }
}   
</script>

<style lang="scss" scoped>
    .question {
        margin: 0 auto;
        max-width: 800px;
        text-align: center;
        border: 3px solid rgb(4, 0, 255);

        &__title {
            background: #edf2ff;
            border-bottom: 3px solid rgb(4, 0, 255);
            margin-bottom: 20px;
        }
        & h3 {
            font-size: 1.5em;
            padding: 10px;
        }

        &__content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        & .btn {
            background: blue;
            color: #fff;
            width: 70px;
            height: 30px;
            box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.678);
            border-radius: 5px;

            &:hover {
                box-shadow: none;
                transform: translate(3px, 3px)
            }
        }
    }
</style>