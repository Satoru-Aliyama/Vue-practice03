<template>
  <div id="app">
    <Header></Header>
    <div class="panel">
      <transition name="flip" mode="out-in">
        <component :is="mode" @answered="answered($event)" @confirmed="mode = 'Question'" class="panel__inner"></component>
      </transition>
    </div>
    
  </div>
</template>

<script>
import Header from './components/Header'
import Question from './components/Question'
import Answer from './components/Answer'
export default {
  name: 'App',
  data() {
    return {
      mode: 'Question',
    }
  },
  methods: {
    answered(isCorrect) {
      if(isCorrect) {
        this.mode = 'Answer';
      } else {
        this.mode ="Question";
        alert('Wrong! Try again!')
      }
    }
  },
  components: {
    Header,
    Question,
    Answer,
  }
}
</script>

<style lang="scss">
  #app {
    max-width: 1000px;
    margin: 0 auto;
    padding: 4%;
  }

  .panel {
    position: relative;
    max-width: 600px;
    height: 200px;
    margin: 100px auto;
    padding: 4%;
    &__inner {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 100%;
    }
  }

  .flip-enter-active {
    animation: flip-in .3s ease-out forwards;
  }

  .flip-leave-active {
    animation: flip-out .3s ease-out forwards;
  }

  @keyframes flip-out {
    from {
      transform: rotateY(0deg);
    }
    to {
      transform: rotateY(90deg)
    }
  }

  @keyframes flip-in {
    from {
      transform: rotateY(90deg);
    }
    to {
      transform: rotateY(0deg)
    }
  }
</style>
